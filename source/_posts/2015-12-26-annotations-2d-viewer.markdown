---
layout: post
title: "Customizing Image Annotations in the 2D viewer"
date: 2015-12-26 18:42
publish: true
comments: false
sidebar: false
categories: 
- conference presentation
---
Whenever you click on an Image or Image Series in the Osirix Database window, the Series is displayed in the 2D-viewer window. The annotations that appear in the window (for example, in the four corners) are specified in Osirix's Preferences, and these are customizable. You can choose to view images without any annotations, or a subset of them. In general, I don't show Teaching Cases with annotations, but when I do, I want a relevant subset only, as the annotations otherwise clutter-up the window.

This guidance document concerns customizing these. I also provide the schemes that I use—which you can download, load into your OsiriX instance, and determine whether they work for you.

 <!-- more -->

___

###Annotations in the 2D-viewer Window###

The screenshot below shows the annotations displayed when I choose the "Basic" setting. Note that the patient's age and gender are displayed (upper-right corner) in addition to other relevant parameters one sees in a clinical PACS-related workstation. If you choose "Full," the Diagnosis is displayed.

{% img center /images/2DWindow.jpg 750 500 2D Window %}

___

###Annotations Preferences in OsiriX###

This image shows the location of this in OsiriX Preferences

{% img center /images/Annotations.jpg 500 500 Annotations %}

Click on it to specify, customize, and load preferences from a file(s).

___

###Customizing Annotations Preferences###

The Preferences window looks like this:

{% img center /images/CustomizeAnnotations.jpg 500 500 Customize Annotations %}

In this window, you can customize annotations for each modality you wish, and specify a Default Scheme. You can drag-and-drop annotations from one location to another, and also specify any Dicom field you wish by using the options in the bottom of the window. (I do not provide detailed guidance for this in this post.)

Note the "Save" and "Load" buttons. Before experimenting with annotation customization, save your current scheme—*for each modality you're going to customize*— so that you can reload it if you mess up.

___

###Loading an Annotation Scheme###

As I mentioned above, you can load a scheme for particular modalities. Do so after you've saved yours.

[Here is a set you can download] [1]. It is a Zip file, which you should unzip on your desktop. Then, modality by modality—for Default, CR, CT, and MR—load these sequentially. Each has the extension "plist."

[1]: http://chestradiologists.org/OsiriXAnnotationsPlists.zip

Explore each so that you can understand how each annotation is specified. Customize them as you wish.

Cheers!


Howard












