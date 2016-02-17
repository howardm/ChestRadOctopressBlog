---
layout: post
title: "Creating a virtual network for OsiriX with ZeroTier One"
date: 2014-12-21 16:44
publish: true
comments: false
sidebar: false
author: Howard Mann
categories: 
- networking
---
Whenever you start OsiriX while connected to a network, it will be assigned an [IP address] [01] permitting one to communicate with other OsiriX instances on the network. You may be connected to the network via an Ethernet cable or, frequently nowadays, via a WiFi Hotspot. The network is typically a so-called [Local Area Network (LAN)] [1], located in an institution or representing the internal network in your home, created by the router you use. 

[01]: https://en.wikipedia.org/wiki/IP_address

[1]: https://en.wikipedia.org/wiki/Local_area_network

The IP address that is assigned to your device will be that used by OsiriX and this address is typically assigned dynamically— that is, it is typically different each time you start your device, depending on which IP addresses have already been assigned to other active devices on the network. To enable reliable communication between OsiriX instances on the network, each instance should have a *static* IP address— one that does not unpredictably change from time to time. 

In addition, devices on a network cannot typically communicate with devices on other local area networks.

Using an application installed on each applicable device—and a means of faciltating a connection between the devices— it is possible (in most situations) to establish a "virtual" network that permits devices on different LANs to communicate privately and securely with the others. This is roughtly analogous, for example, to using Apple's [Back to my Mac] [2] (or other similar applications) utility to connect your laptop to another Mac at home while you're in another location.

[2]: http://support.apple.com/en-us/HT4907

This is the subject of this guidance document.

<!-- more -->

___

###The value of a virtual private LAN###

These are several reasons you may want to create a virtual LAN:

* to establish a [Teaching File Server] [3] from which selected colleagues can retrieve cases.
* to share a particular OsiriX Database with selected colleagues at different institutions in the context of a research collaboration. When configured correctly, individuals can both send and retrieve cases from the other OsiriX instances on the network. 
* to retrieve cases from a Mac in your office at work while you're at home.

I'm sure you can now think of additional similar situations in which a virtual network involving OsiriX will be of use to you!

[3]: http://chestradiologists.org/blog/2013/03/22/osirix-server/

___

###Establishing a private and secure virtual network###

[ZeroTier One] [4] permits the creation of such a network. Importantly, it permits the creation of the network without complicated configuration. You do not have to be a hacker. It just works!

[4]: https://www.zerotier.com

This is the process which—without exaggeration—takes minutes:

####Creation of the Network####

One person ("Administrator") initially installs the application and manages the membership of the network. He establishes an account at the ZeroTier One website. At the time of this writing, the cost is $4 a month (for unlimited members) when the number of devices on a network exceeds ten—a very modest charge.

The following screenshot shows the Management Panel:

{% img center /images/ControlPanel.jpg 750 500 ControlPanel %} 

The IP address range you choose for your network is not critical. In the example above, you can see that I chose the 22.x.x.x range.



####Joining the network####

Thereafter, each person who wants to join the network installs the application on his device and requests the Administrator to explicitly authorize his device (identified by its unique "address") on the network. 

Once you are an authorized member of the network your personal Panel looks like this:

{% img center /images/PrivatePanel.jpg 750 500 PrivatePanel %}

___

####Your OsiriX instance on the virtual network####

The following point is worth stressing: Your OsiriX instance may be a member of more than one network simultaneously. Here is my laptop OsiriX on three networks, with three IP addresses, one of which is related to the virtual network:

{% img center /images/ListenerLAN.png 750 500 ListenerLAN %}

___

####Configuring your OsiriX to securely share cases####

In most instances, it is sufficient to establish an OsiriX Web Portal using your virtual network IP address. Authorized members will be able to login to it, search for, and download cases.

{% img center /images/LANWebServer.png 750 500 LiANWebServer %}

___

####Additional Security-Related Configurations###

A private ZeroTier One network itself is very secure. All data transmitted across the virtual network are first encrypted on each device before transmittal. No data are stored on any cloud-based server or other device. The encrypted data are essentially transmitted from device-to-device (peer-to-peer).

If you're inclined, additional security-related information concerning a ZeroTier One network [is available here.] [6]

[6]: https://github.com/zerotier/ZeroTierOne/wiki/ZeroTier-One-Security-FAQ

OsiriX is great in that additional measures may be taken to further secure Web access to cases on any OsiriX instance. Consider the situation shown on the following image

{% img center /images/ProjectDatabase.png 750 500 ProjectDatabase %}

I have selected two databases on this OsiriX instance. (Command-click to select.) One is the Local Database. The other is a separate database I created for a project. (Click File: New Database folder...) The *Comments* tag in the meta-data for each case in the project's database is "researchproject"

Now I can enable access to these cases only via the virtual network (as long as the device is online, of course) as shown below:


{% img center /images/MoreSecurity.png 500 750 MoreSecurity %}

___

</br>

Please contact me if you have any questions or if you have used ZeroTier One for a particularly useful or interesting purpose.

Cheers!

Howard



































