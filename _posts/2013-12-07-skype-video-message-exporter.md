---
title: Skype Video Message Exporter
categories:
- projects
tags:
- skype
- video message
---
A few days ago, I found out that you can send video messages to people via Skype. Someone asked me if I knew of a way to export them from Skype. (That way you can watch them while offline, back them up for later, or whatever else you might want to do.)

After searching around the web for a while, I realized that there is no such feature at the moment. I also saw many <a href="http://community.skype.com/t5/Windows-desktop-client/Save-a-received-Video-Message/td-p/1716649">people suggesting</a> an SQLite browser add-on for firefox.

It turns out that Skype uses a sqlite database to save messages and other information. On OSX, the main database file is located under `~/Library/Application Support/Skype/skype_username/main.db`

Inside the file is a table called VideoMessage, which contains the URL for all received video messages. What people were doing was finding the URL using the sqlite browser, then downloading each file individually. Another problem was that those links expire after some time, so if you haven’t viewed the video in Skype in the recent past, they won’t work. Since this method is a bit complicated for most users, I decided to automate it.

My first version consisted of a bash script that used <strong>find </strong>to get the database file, then called <strong>sqlite3 </strong>to get the urls, and generated an html file with links to the videos. It worked, but it still wasn’t as easy as it could be.

The next/last step consisted of writing an Objective-C app to do it all.

{% include image.html
            img="images/wp/Screen-Shot-2013-12-07-at-4.28.34-PM-640x249.png"
            title="VideoMessageExporter Screenshot"
            caption="VideoMessageExporter Screenshot"
            url="https://alvarop.com/images/wp/Screen-Shot-2013-12-07-at-4.28.34-PM.png" %}

The application automatically finds the database file (or files, if there are multiple Skype accounts). After that, it opens each one and gets the video message info to display. The users can then select the messages they want and download them all at once to the desktop.

You can download the latest OSX build here: <a href="https://github.com/alvarop/VideoMessageExporter/releases">VideoMessageExporter Releases</a>
For more info and all the sources check out the <a href="https://github.com/alvarop/VideoMessageExporter">github page</a>.
