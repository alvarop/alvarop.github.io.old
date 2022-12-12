---
title: Migrating Blogger to Wordpress Permalinks
categories: []
tags: []
---
I recently migrated my blog from blogger to WordPress. The migration was extremely easy with the automatic importer in WordPress. The only problem is that every single link on the web is pointing to the blogger generated permalinks, which do not match the new WordPress ones.

Since I still get some traffic from other sources, I decided to come up with a method to have the old links redirected to the correct new ones. If you have a list of the old url and the new url, you can use apache's <a href="http://httpd.apache.org/docs/trunk/rewrite/remapping.html">mod_rewrite </a>to automatically redirect the pages without the user ever noticing. The problem here is coming up with that list of equivalent urls without spending hours doing it by hand.

The first problem dealt with getting a list of all the old blogger permalinks. Luckily, I found a '<a href="http://www.bloggerplugins.org/2009/07/table-of-contents-widget-for-blogger.html" target="_blank">plugin</a>' that generates a table of contents with links to every post. Unfortunately, it does it with JavaScript, so you can't just right-click the page and view source to get the links. The way to do it with chrome is as follows:

First right-click over the generated links and select "inspect element".

{% include image.html
            img="images/wp/1_inspect_element.png"
            title="Inspect Element"
            caption="Inspect Element"
            url="/images/wp/1_inspect_element.png" %}

Once the inspect element window appears, right-click on the top HTML tag and select "Copy as HTML". This will let you copy the JavaScript generated HTML. (If you had just clicked view-source, it might not have included that.)

{% include image.html
            img="images/wp/2_copy_as_html.png"
            title="Copy as HTML"
            caption="Copy as HTML"
            url="/images/wp/2_copy_as_html.png" %}

Paste the HTML onto your favorite text editor. I saved it as "toc.html".

{% include image.html
            img="images/wp/3_notepad-527x480.png"
            title=""
            caption=""
            url="/images/wp/3_notepad.png" %}

The next step is to get all the 'new' links from the WordPress site. You can export an xml file with all the information in the WordPress settings. I saved that one as "wpexport.xml".

{% include image.html
            img="images/wp/4_export_wordpress_xml.png"
            title="Wordpress Export"
            caption="Wordpress Export"
            url="/images/wp/4_export_wordpress_xml.png" %}

Now that there are two files with the links buried in them, we need to extract them and match them. I wrote a quick <a href="https://github.com/alvarop/alvarop-scripts/blob/master/blogger_to_wordpress_links/blogger_to_wordpress_links.pl">perl script</a> that reads both files, takes the urls, matches as many as it can, and spits out a csv file.

{% highlight bash%}
$ perl blogger_to_wordpress_links.pl > links.csv
{% endhighlight %}

Most of the urls were automatically matched, but a few were not, so I opened up the csv file in excel and filled out the rest. (It puts all of the unmatched urls at the bottom of the file so you only have to cut and paste, not re-type).

{% include image.html
            img="images/wp/5_csv_link_list.png"
            title="CSV List"
            caption="CSV List"
            url="/images/wp/5_csv_link_list.png" %}

Ok, so now I have a csv file with URL's, but what I really need is a .htaccess file to actually do the work. I wrote <a href="https://github.com/alvarop/alvarop-scripts/blob/master/blogger_to_wordpress_links/csv_to_htacces.pl">another script</a> to do that.

{% highlight bash%}
$ perl csv_to_htacces.pl links.csv > .htaccess
{% endhighlight %}

The .htaccess file should now redirect any traffic pointed at the 'old' blog and send it to the correct page on the new WordPress one. I did have to manually add a rule for my 'about me' page, but it sure was easier than manually doing 90-something posts! The .htaccess file should end up looking something like this:

{% highlight apache%}
RewriteEngine  on
RewriteRule 2007/05/first-week-of-summer-part-1-of.html http://alvarop.com/2007/05/first-week-of-summer-part-1-of [R]
RewriteRule 2007/05/first-week-of-summer-part-2-of.html http://alvarop.com/2007/06/first-week-of-summer-part-2-of [R]
RewriteRule 2007/05/mid-exam-week-update.html http://alvarop.com/2007/05/mid-exam-week-update [R]
RewriteRule 2007/05/new-phone.html http://alvarop.com/2007/05/new-phone [R]
RewriteRule 2007/05/one-down-four-to-go.html http://alvarop.com/2007/05/one-down-four-to-go [R]
RewriteRule 2007/05/slow-weekend.html http://alvarop.com/2007/05/slow-weekend [R]
RewriteRule 2007/06/5-days-left.html http://alvarop.com/2007/06/5-days-left [R]
RewriteRule 2007/06/boring-friday-and-rest-of-week-update.html http://alvarop.com/2007/06/boring-friday-and-rest-of-week-update [R]
RewriteRule 2007/06/early-morning-update.html http://alvarop.com/2007/06/early-morning-update [R]
{% endhighlight %}

That's it!
