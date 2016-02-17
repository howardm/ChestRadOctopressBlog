---
layout: post
title: "A Customized Teaching File Anonymization Scheme for OsiriX"
date: 2014-11-14 
publish: true
comments: false
sidebar: false
author: Howard Mann
categories: 
- anonymization
---
Sharing or publishing an OsiriX  Teaching File case requires antecedent anonymization of the meta-data associated with it. After importing a case into OsiriX's Local Database, one can use OsiriX's anonymization utility to accomplish this. When you first install OsiriX, the "default" anonymization scheme is insufficient for complete removal of all the personal information (about the patient, but also the ordering physician, among others) in the so-called Dicom "Header. "

In this guide, I'll describe a method you can employ to quickly configure a comprehensive scheme to get you going. It'll remove the great majority— but not *always* all —of the personal information items present in the meta-data. If you need to manually remove residual items, [look at the relevant part of this guide] [2] for a description of how to do this.

[2]: http://chestradiologists.org/blog/2013/03/23/title/


<!-- more -->
___
<br/>
###OsiriX Anonymization Window###

The customized anonymization window should look like this:
<br/>
{% img center /images/AnonScheme.png 750 500 AnonScheme %} 

Note the button in the top-left corner. I've (arbitrarily) named this `WebConfCustom.` Once you have this scheme, click the button to select it.

While one can manually edit the default scheme to achieve this, it's a bit cumbersome to find each Dicom field (by using the "Select a DICOM tag..")  to add, one-by-one.  

___

<br/>
###The Osirix .plist Preferences File###

This file contains the anonymization scheme as well as all the other preferences you've configured for your OsiriX instance. We're going to edit this file directly to add the `WebConfCustom` scheme.  To do this, go first to OsiriX: Preferences: General.
<br/>
{% img center /images/OsiriXPref.png 750 500 OsiriXPref %} 

Start by clicking `Save Preferences...` and save one copy to your Desktop and one somewhere else in case you make a mistake. You're going to edit the copy on your Desktop.

Open the file with TextEdit and scroll down until you see the section starting with this line: 

`<key>anonymizeTemplate</key>`

Each anonymization scheme has the following format: `<key>Name</key>` followed by the content between an opening `<dict>` and a closing `</dict>` You're simply going to add another one to those already there. Once you understand this format, [download this file] [1], open it, copy-and-paste the scheme in the proper place in your file, and save it. 

[1]: http://chestradiologists.org/AddAnonScheme.rtf

That's it!

 Now go back to OsiriX: Preferences: General and click the `Load Preferences...` button and choose your edited file. The new `WebConfCustom` will now be there and selectable for you to use.
 
___
<br/>
If you make a mistake, you can always load the copy you saved, and contact me if you can't figure out what happened.

Cheers!
 
 
 
 



















