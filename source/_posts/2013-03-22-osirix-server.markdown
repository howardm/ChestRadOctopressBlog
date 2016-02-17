---
layout: post
title: "Configuring and Operating an OsiriX Teaching File Server"
date: 2013-03-22 23:32
comments: false
sidebar: false 
categories: 
- osirix teaching file server
- teaching file network
- anonymization
- sharing teaching cases
- backup strategies
---
####Updated in December 2015####

In this guidance document I'll describe how to configure and operate an OsiriX-based Teaching File Server that will enable you to share your cases with colleagues. 

If you and your colleagues put your individual servers on an Internet-based network , each network member will, in effect, have a Teaching File consisting of the cases on all the servers.

How this works will become apparent as you read this document. 

  
###Contents###

* Hardware and Software Considerations
* Network Considerations
* Backing up the data on your Server
* Getting and anonymizing DICOM cases
* Configuring OsiriX on your Server
* Understanding a JPEG 2000 Teaching Server Network
* Querying a Server for Teaching Cases
* Exporting a case to share with colleagues

<!-- more -->

___
<br />
###Hardware and Software Considerations ###

A Mac mini or iMac is fine as a Server. There is no need to utilize [OS X Server] [1]. To use OsiriX for the purpose described in this document, you'll need to purchase the non-free version. OsiriX Lite, the free version, has too many functional limitations, substantially increased since I wrote the first version of this guidance. Explore the [Pixmeo Website] [2] for purchase options, including the possibility of a Site License for your department or practice.

[1]: https://www.apple.com/osx/server/
[2]: http://pixmeo.pixmeo.com/store.html


If you can afford it, purchase a device with a [SSD drive] [3], and at least 8GB of RAM. The combination of a SSD drive and El Capitan (the latest version of the OS X Operating System as of Late 2015) will optimize the serving of images.

[3]: https://en.wikipedia.org/wiki/Solid-state_drive

The average size of a Teaching Case on my Server is around 30-50 MB, the case being stored in a compressed state (JPEG 2000 compression). Many of my cases contain multiple CT, CT-PET and/or MR Series, each Series sometimes consisting of several hundred thin-section images. 


If you choose a Mac mini, you can operate it via remote control using the [Screen Sharing] [5]  VNC application that comes with OS X.  Other third-party [VNC] [6] applications are available for this purpose but are not, as far as I know,  better than Screen Sharing for this purpose.  

[5]: http://osxdaily.com/2012/10/10/remote-control-mac-screen-sharing-os-x/
[6]: https://en.wikipedia.org/wiki/Virtual_Network_Computing

Note that you can use iCloud and [Back to my Mac] [5b] for screen sharing as long as both devices are configured to use the same iCloud account. A guide for this is [here.] [6a]

[5b]: http://support.apple.com/kb/ht4907
[6a]: http://chestradiologists.org/ScreenSharingontheMac.pdf 

I suggest the following password-protected configuration (System Preferences) for Screen Sharing:

{% img center /images/ScreenShare.jpg 750 750 Screen Share %}

Here is an image of me working with my Mac mini Server from home:

{% img center /images/Screenshare1.jpg 750 750 Screen Share %}


___
<br />

For an OsiriX server, you need to institute a number of actions and specify particular system-wide preferences.

General instructions and guidance are available  [at this Web page.] [7]

[7]: http://www.osirix-viewer.com/PACS.html

Here is a summary of the things you should do:

I want to be sure that OsiriX is always running and is restarted in the event of an elecricity failure or an unexpected application crash.

[8]: http://www.peterborgapps.com/lingon/

I use the application [Lingon 3] [8] for this purpose. Here is a sceenshot of it running on my server:

{% img center /images/Lingon.jpg Lingon %}

If you use Lingon for this purpose, specify that OsiriX is initiated at login/load and is "kept running." 

2. In System Preferences: Energy Saver, select " Start up automatically after a power failure." Move the slider for "Computer Sleep" to "Never" and select "Wake for network access." Do not select " Put hard disks to sleep when possible."

3. In System Preferences: Users&Groups: Login items on your Mac, make sure that OsiriX is in the List. If you use Lingon, then it need not be. 

4. If your Server is a Mac mini which is not connected to a display, go to System Preferences: Desktop&Screen Saver, and change the option on the Screen Saver to `Never` which otherwise sometimes interferes with Screen Sharing. Change your Destop Background to a simple solid color.

5.  In System Preferences, select automatic log-in (Users & Groups, Login Options, Automatic login)

6. Activate the "Server mode" in OsiriX. This mode will hide the GUI, and OsiriX will never present a blocking window to the user (nobody will look at the server monitor to click the "OK" button...). Go to OsiriX Preferences: Listener, Server mode.

7. When an application on the Mac crashes, a Crash Reporter often comes up, asking you to respond and, optionally, to send a report to Apple. For a Server, you're not there to respond to this. To prevent this from happening, open the Terminal utility, select-and-copy the following, paste it at the command line and hit "return":

`defaults write com.apple.CrashReporter DialogType Server`

Like this:

{% img center /images/Terminal.jpg 750 750 Terminal %}

You can still see and inspect the Crash Reports in the Console app if you wish.

If you ever want to change this back to the default mode, type this at the command line:

`defaults write com.apple.CrashReporter DialogType Developer`


___
<br />
###Networking Considerations ###

The Server needs to have a [static (fixed) IP address] [8] and the fastest connection speed to the Internet as reasonably achievable. There are three basic options for accomplishing this:

1. Locating your Server at home
2. Locating your Server at work
3. Locating your server at a [Colocation Facility] [CF]

[8]: https://en.wikipedia.org/wiki/Static_ip_address#Static_IP
[CF]: https://en.wikipedia.org/wiki/Colocation_centre

####Home server

One purchases a package from an Internet Service Provider that includes a Static IP address(es) and a certain bandwidth. Availability and affordability are considerations for this option.

####Server at work

In this scenario, you server will be physically connected by ethernet cable to the wired hospital [Local Area Network] [9] (LAN).  Your IT department should be able to reserve a particular IP address for your server by means of so-called *dynamically assigned static IP addresssing*. Ask for this. This is very convenient as you'll then easily be able to send cases on your laptop to it from anywhere. My Mac mini Server is in my office and I DICOM-send cases to it from anywhere in the hospital such as the Reading Room where I work each day. If your Server's LAN IP address is fixed you'll also be able to start the OsiriX Web Server with that address as the **Public address**  and the Web Portal will then always be available at that address, which you can then share with departmental colleagues.

[9]: https://en.wikipedia.org/wiki/Local_area_network

Your hospital may also provide a means to connect to the hospital network from the outside via a VPN application of some kind . If so, you'll first connect to the network via the VPN and then have access to your Server via its fixed LAN address.  The following image shows a browser-based VPN application I use to connect to my institution's network:

{% img center /images/HospitalVPN.jpg Hospital VPN %}

####Connecting to your server ####

In order to connect to your office Server, you can create a Virtual Private Network using an application called ZeroTier One. Review the [guidance document] [9a] on this website about this.

[9a]: http://chestradiologists.org/blog/2014/12/21/creating-a-virtual-local-area-network-for-osirix-with-zerotier-one/

In this scenario, your Server will be assigned a network-associated static IP address and other clients in the private network only will be able to connect to it. 

Your Server's OsiriX instance may have multiple IP addresses simultaneously, one of which is your address on the ZeroTier One network, as shown in this portion of my Preferences:Listener panel:

{% img center /images/ListenerPrefs.jpg Listener Prefs %}

The advantages of this option are:

* You will have access to your server at the hospital on a high-speed and high-bandwidth wired LAN
* You'll have your institution's fast bandwidth connection to the Internet to facilitate retrieval of cases from the Server from outside the hospital. 
* You'll be able to connect to your Server from anywhere (including outside the hospital) via Screen Sharing using the ZeroTier One network IP address
*  You'll be able to connect to the Server's OsiriX Web Portal via either the Portal's LAN IP address (while at the hospital) or via the ZeroTier One network (while outside the hospital)
* You'll not have to purchase a static IP address package from your Internet Service Provider

___
<br />
####Server at a Colocation Facility

At first, this idea may seem silly as your computer has to be shipped to another physical location. However, there are entities that specialize in colocating Mac minis, such as [Mac mini Colocation] [11] and [Mac mini Vault] [12]. They provide you with a static IP address, and offer fast Internet connections at a reasonable price. You can manage your server remotely using Screen Sharing (or a VPN application they'll provide you) as I mentioned above. 

[11]: http://macminicolo.net/
[12]: http://www.macminivault.com/

###Update: May 2014###


 I have moved my Mac mini from the hospital to a colocation facility— [Mac mini colocation][11]. The upload speed from there to the Internet is much faster than with the usual home setup, which is great for serving up cases. Here is a screenshot showing upload and download speeds at the facility. (You can test your own speeds at: beta.speedtest.net)
 
 {% img center /images/SpeedTest.jpg Speed Test %}
 
 [11]: http://macminicolo.net/
 
___
<br />
### Backing up the Server 

I strongly suggest that you employ *two* concurrent means of backing up your OsiriX Data Folder: 1) to an attached external disk utilizing software such as Time Machine and 2) to an account in the Cloud. Nice options for Cloud storage are [Crash Plan] [13], [Backblaze] [13a],  and [Amazon Glacier with Arq] [14].  (Amazon Glacier pricing is only $.01/GB per month, as of this writing.) It's easy to schedule automatic backups with these. 

[13]: http://www.crashplan.com/
[13a]: http://www.backblaze.com
[14]: http://www.haystacksoftware.com/arq/index.php

___
<br />
### Getting and anonymizing DICOM cases 

If your PACS application permits you to export a case in [DICOM format] [15] with one click, the most efficient method is to ask your IT department to assign your laptop (or another device other than your Server) a static IP address as well, as I described above. Then, register your OsiriX laptop as a DICOM-node on the PACS administration module. When your laptop is connected to the network via an ethernet cable, you will: 1) DICOM-send the case to your laptop OsiriX, 2) anonymize the case on your laptop, and 3) DICOM-send the anonymized case to your Server.  Otherwise, you'll have to use another method such as a USB thumb drive to transfer the case to your laptop. 

[15]: http://www.saravanansubramanian.com/Saravanan/Articles_On_Software/Entries/2010/2/10_Introduction_to_the_DICOM_Standard.html

	Remember: A non-anonymized case should not be on your Server at any time. 
	


Here is a screenshot of me sending a case to my laptop OsiriX directly from our Philips iSite PACS:

{% img center /images/DICOMExport.jpg DICOMExport %}


I always have my laptop connected by ethernet cable to the LAN at the Workstation I'm working at, so I can do this as I perform my daily work in the Reading Room. If I have time right then, I'll anonymize it, *check the meta-data again to verify that the anonymization of personal information is complete*, and DICOM-send it to my Server. Otherwise, I'll do this step another time. 

___
<br />

### Anonymizing cases -- three methods

**Using the OsiriX anonymizer** 

Here is a minimum scheme:

{% img center /images/Anon.jpg Anon %}

Add to these as necessary as you inspect the Metadata as I indicate below. 


 `Tip: When you use the "Merge" command in OsiriX to merge all the Series of a particular case before anonymizing it, the component Series will be split again when you DICOM-send or Retrieve it from the Server. This is annoying! Prevent this by putting the Case Number in the DICOM Tag "StudyInstanceUID", as indicated above in the graphic. `
	
With all the DICOM tags I've added to this scheme most cases are anonymized such that all personal information is removed. But not always. Scroll through the Metadata of a Series of a case to be sure that none is left. If any remains, use the next manual method to remove it. You can also use the manual method to edit any particular field(s) in the DICOM Header (Metadata). 

___
<br />
**The Manual Method**

OsiriX permits one to edit any particular field in the DICOM header. This is a three-step process as indicated below:

1. Activate the editing function by clicking on `edit`.
2. Double-click on an entry to edit it and hit return. Edit other items as necessary.
3. Click `Apply` specifying the `Study` level so that all the Series of the Case are changed.

{% img center /images/ManualEdit.jpg Manual Edit %}


___
<br/>
**Using Dicom Anonymizer to anonymize cases**

If you do not use OsiriX to anonymize a case, a great application to do this is *Dicom Anonymizer*.  Indeed, it's easiest to anonymize a case on your desktop with this *before* importing it into OsiriX.
<br/>
{% img center /images/DICOManonymizerWindow.png 500 500 Window %}
<br/>

Review my [guidance document][22] on this web site for details on its use.

[22]: http://chestradiologists.org/blog/2014/05/26/title/


___
<br />
**Removing personal patient information embedded in an image**

Sometimes, for example, with an ultrasound image series, PHI is embedded in the image and cannot be removed by editing the DICOM header. In this case, the relevant portion of the image has to be removed, the resultant image saved as a separate Series, and the original Series deleted.

The process is as follows:

1. Define the area to be *retained* with the `rectangular ROI tool`. In the image below, I'm using this technique to exclude extraneous markers from a bedside chest radiographic image. The same process may be used for an ultrasound or nuclear medicine series containing many images.
2. Click on the Shutter Tool icon in the toolbar. If the icon is not there, right-click on the toolbar, choose `Customize Toolbar` and drag it there. 
3. This image demonstrates what you see just before you invoke the Shutter Tool

{% img center /images/ShutterTool.jpg 650 650 Shutter Tool %}

Next steps...

4. Now that everything outside the ROI has been removed, use the Zoom and Pan tools to resize and center the resultant image as necessary in the window.
5. Hit `Command-E` to save this as a new Series (named as you choose) in the case.  For Image Format, specify `as displayed in 16-bit BW` before clicking OK. 
6. Delete the original series.

If you want to view an excellent video of this process applied to an ultrasound examination, do so right here (Credit: Dr. Mary Roddie, OsiriX U.K. User Group):

{% youtube UdxO_LKrxpg %}
___
<br />
If you have a single JPG image with embedded personal information that you want to import into an OsiriX case, use the Preview application that comes with every Mac to crop out the information (or blacken it) and then import it into the case with the OsiriX menu item: `Plugins...Database...JPEG to DICOM` utility, specifying the `Meta-data: from the selected study in Database window` option when doing so. 

___
<br />
### Configuring OsiriX on the server 

You need to configure certain items in OsiriX Preferences differently for a Server compared to a Retrieving Workstation. The scenario is analogous to that in your department: Your PACS Server delivers images on demand to Workstations; the former is equivalent to your OsiriX Teaching File Server and the latter are the devices retrieving images from it. The options you should specify in your OsiriX Preferences are indicated on the following screenshots from my Server:

___
<br />
{% img center /images/Listener.jpg Listener %}


It's best if you do `not` choose the option to broadcast the existence of your Server via the Bonjour protocol. If you do, any person with OsiriX on the network may see your Server's Dicom-node parameters (AE Title, IP address and Port) by hovering the cursor over it in the Sources List and try to query your Server for cases via the Query/Retrieval window, as explained further below:

{% img center /images/AETitleIP.jpg AETitle %}

Instead of this, manually add it to the List of Shared Databases on your laptop's OsiriX as shown here:

{% img center /images/OsiriXDatabases.jpg Osirix Databases %}


___
<br />
{% img center /images/Locations.jpg 500 500 Locations %}

___
<br />
When you specify "WADO" above, you'll need to specify additional items as indicated here:

{% img center /images/Locations1.jpg Locations1 %}

<br />
`It's very important to specify retrieval using the **Original Syntax** which is JPEG 2000. If you do not, the server will decompress the images before sending them diminishing the transfer efficiency. In addition, the decompressed images will then remain on the server in a decompressed state, slowing the retrieval speed for subsequent retrieval requests. `

___
<br />
###Osirix Web server 

{% img center /images/WebServer.jpg 500 500 Web Server %}


___

##Understanding a JPEG 2000 Teaching Server Network 

As I alluded above, transmission of data over the network is facilitated by the use of data compression with the JPEG 2000 algorithm. This should not be conflated with the production of JPG format images. It is a compression scheme that permits lossless and lossy compression. The degree of compression may be stipulated in OsiriX Preferences:General. 

The default values may be changed to achieve greater compression, without a perceptual difference in quality. I highly recommend you do this as it will allow you to store more images on your storage medium and your cases will be retrieved faster over the network. Review the [guidance document on this web site] [17a] for details. It's easy!

[17a]: http://chestradiologists.org/blog/2014/05/31/jpeg-2000/

Here is the default compression scheme I suggest you use:

{% img center /images/CompressioninOsiriX.png 750 500 JPEG Compression %}

<br/>

Just get in the habit of right-clicking on a case after you've anonymized it and choosing "Compress DICOM files."

For best performance and transmission efficiency, the network should be configured such that all aspects involve the JPEG 2000 transfer syntax. The intended result is that decompression of the images for viewing will occur once only: after the data have been received by the requesting Workstation. When using the [WADO] [18] (Web Access for Dicom Objects) protocol for retrieving cases from a server, one should specify, as indicated in the graphics above, transmission via the Original Syntax (Send Transfer Syntax)  which, in turn, should be specified (in Preferences: Locations) as JPEG 2000.  

[18]: https://www.research.ibm.com/haifa/projects/software/wado/

For further details about this, read the relevant part of [this PDF document] [19]

[19]: http://www.osirix-viewer.com/OsiriX%20JPEG2000.pdf 

Here is a graphic summary of the requisite setup:

{% img center /images/JPEG200Network.jpg JPEG 2000 Network %}


If you're unsure whether a particular case on your server is compressed, compress it manually as shown here:

{% img center /images/ManualCompression.jpg Manual Compression %}


___

##Querying a Server for Teaching Cases 

There are two basic ways of querying a Server for cases and retrieving them: 

1. Using the OsiriX Web Portal
2. Using the OsiriX Query/Retrieval window

###The Web Portal

After you login to the Web Portal and find a case you want to retrieve, there are three choices as shown in this graphic:

{% img center /images/WebPortalRetrieval.jpg Web Portal retrieval %}


1. WADO retrieval directly to your OsiriX database
2.  Download case as a Zip file
3.  Download the case and view it with the Weasis viewer.

WADO retrieval is a great option. Indeed, you could right-click on the OsiriX icon and choose `Copy Link Location` and send the link to any one with access to your server to allow him to use the link to download that case:

{% img center /images/CopyLinkLocation.jpg 750 550 CopyLinkLocation %}


Allowing others to retrieve cases via the Web Portal is a good option because you can control which people have access (username and password) to it and control whether they can upload cases to it or share cases with others. All these options may be specified when you select this method of control:

{% img center /images/WebServerControl.jpg Web Server Control %}

 
 ___
<br />
If you select to view the case with Weasis, the java-based Weasis Viewer will automatically be downloaded to your computer, started, and the case retrieved into it (You have to permit java applications to be downloaded and run on your computer.) . It's also a great way for someone without OsiriX to view the case. 

___
<br />
###Using the OsiriX Query/Retrieval window 

This is a great way to query multiple OsiriX Servers simultaneously as shown here where I'm querying my and a colleague's servers for an "aortic..." case:

{% img center /images/QueryRetrieve.jpg Query Retrieve %}

`Reminder: Before retrieving a case using this method, check again to be sure you have specified the WADO protocol and Original Syntax in your OsiriX Preferences: Locations for the server you're about to retrieve from.` 
___
<br />
###DICOM-sending a case to a colleague's server

You can DICOM-send a case to another member's server when saving it to our own. This is easy to do. Just select the case in your Database Window and drag-and-drop it over the icon for it in the Sources List as shown here:
	
{% img center /images/DragDrop.jpg DragDrop %}

___

##Exporting a case to share with colleagues 

In addition to the methods for directly sharing cases via the network I described above, you can export a particular anonymized case to share with colleagues, for example, via [Dropbox] [20] or a similar cloud-based service:

1. Create and label a new folder on your desktop.
2. Right-click on a case (or select several cases) and choose `Export to DICOM File(s)`
3. Navigate to and select the folder you created on your Desktop and specify the options shown here:

[20]: http://www.dropbox.com/home

{% img center /images/ExportCases.jpg 750 Export cases %}

`Important: Note the checkbox for Compressing files with JPEG above. Select it. If you've forgotten to compress your cases (as I mentioned above), this will achieve compression at this point.`

Now drop the folder into your Dropbox and email them a link to download it once it has been uploaded to the Dropbox server. 

