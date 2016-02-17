---
layout: post
title: "Showing a case in OsiriX during a Keynote presentation"
date: 2013-11-01 19:55
publish: true
comments: false
sidebar: false
author: Howard Mann
categories:
- keynote
---
</br>
When giving a radiology talk using Keynote it is usual to utilize selected images and videos. Sometimes it would be useful to scroll through an entire (or multiple) CT, PET-CT or MRI Series, with the ability to change the display parameters in realtime. It is not currently possible to embed a DICOM file Series in Keynote, but it is possible to call a particular case in OsiriX directly from Keynote, show the case in OsiriX, and then return to the Keynote presentation. In this way, one can toggle efficiently between Keynote and OsiriX (using the keyboard shortcut `command-tab`) without disrupting the overall flow of the presentation. 

<!-- more -->

###A protocol for calling a case in OsiriX

It is possible to initiate actions in OsiriX from another application through the use of a particular protocol called [XML-RPC] [1] and a browser. I do not understand the technical or programming details, but the concept is straightforward: one sends OsiriX an instruction from Keynote via a server/browser combination. An additional application is required to provide the requisite server and associated code on your computer. Otherwise, it's only a matter of associating text on a Keynote slide with a hyperlink that contains a relevant instruction in the proper XML format. Note that the browser can only initiate actions on an instance of OsiriX running on the same computer.

[1]: http://www.osirix-viewer.com/Documentation/Guides/Development/index.html#XML_RPC_support

The procedure is as follows:

___
</br>

**Turn on the HTTP XML-RPC server at the bottom of OsiriX Preferences: Listener**

{% img center /images/activateserver.jpg 750 750 Activate server %}

___
</br>
**Download and configure the SimpleHTTPServer**

This application was made by Juan Jose Cermeño Portet, a Medical Imaging Consultant & Software Developer at [Turyon Projects] [2] who has graciously made it freely available. Download it [here] [3].

[2]: http://www.turyon.com/index.php
[3]: http://chestradiologists.org/SimpleHTTPServer.app.zip

Run the application. (If you get a warning message about running an application from an "unknown developer," just go to your Mac's System Preferences: Security & Privacy panel to permit the application to run.) It looks like this:

{% img center /images/HTTPserver.jpg 750 750 HTTP server %}

If you need to change the port number, you may need to quit the application and restart it. The application must be running during your presentation. 

___
</br>
**Put the cases you're going to show in your OsiriX Local Database**

Make sure that the cases you're going to show are in the Local Database of OsiriX which must be running during your presentation. 

___

</br>
**Insert a relevant hyperlink in text in a Keynote slide**

This is demonstrated in this graphic:

{% img center /images/keynotehyperlink.jpg 750 750 keynote hyperlink %}

In this example, I'm calling a particular Series from a Case in OsiriX indicated by its SeriesInstance UID in the link:

seriesInstanceUID&name=`1.3.6.1.4.1.19291.2.1.2.4045201004198100004`

Get the number from the meta-data of that Series in OsiriX as follows:

{% img center /images/Seriesnumber.jpg 750 750 Series number %}

Double-click on that number and copy-and-paste (command-C; command-V) it into the proper location in the hyperlink.

___
</br>

**Examples of XML HTTP links for calling cases in OsiriX**

Here are examples of several properly-formatted links to enable you to call particular Studies or Series in OsiriX:

Open a particular study using the patient ID and close all the previous OsiriX viewers:

`http://localhost:12345/keynote?type=patientID&name=[insert patient ID here]&close=1`

Open the first series of the first study of patient with patientID=08291 and close all the previous OsiriX viewers:

`http://localhost:12345/keynote?type=patientID&name=08291&table=Study&close=1`

Open the first series of the first study of patient with name=MANIX and closes all the previous OsiriX viewers:

`http://localhost:12345/keynote?type=name&name=MANIX&table=Study&close=1`

Open a specified study and close all the previous OsiriX viewers:

`http://localhost:12345/keynote?type=studyInstanceUID&name=[insert number here]&table=Study&close=1`

Open a specific Series and close all previous OsiriX viewers:

`http://localhost:12345/keynote?type=seriesInstanceUID&name=[insert number here]&table=Series&close=1`

___
</br>

Here is a nice video of this process made by Dr. Sameer Shamshuddin of the [OsiriX-UKUser group] [4]

[4]: https://sites.google.com/a/osirix-ukusergroup.org/www/

{% youtube phQXUw0hWjk %}

</br>
___
</br>

Enjoy!





















 
















