---
layout: post
title: Detailed impressions of the Chromebook Pixel
date: '2014-02-22 07:35:46'
---

A few weeks ago I bought a used Chromebook Pixel. As I [previously](https://blog.dictvm.org/chromebook-pixel-1/) mentioned, it is a quite capable machine. 

![Chromebook Pixel Keyboard](/content/images/2014/Feb/IMG_20140220_014221.jpg)

## The Hardware

The more I use it, the more I learn to appreciate the sheer quality of the keyboard. The Macbook Pro’s keyboard feels a bit cheap and clumsy in comparison. Its display is also more glossy than the Pixel’s. Performance wise, the Macbook Pro is totally superior in almost all aspects: It's available with an i7, it comes with two 10GBit-Thunderbolt-Ports, two USB 3.0-ports and the HDMI-port allows easy plug’n’play to any TV you can imagine, while the Pixel only supports a Micro-DisplayPort. The Pixel shines with its sturdiness. The boxy construction of the shell feels robust and the dark grey aluminum looks even better than one might assume by looking at Google’s renders on its [Chromebook Pixel-site](https://www.google.com/intl/de/chrome/devices/chromebook-pixel/). The Macbook looks thinner due to the rounded design of the device, but in direct comparison the Pixel wins at about a Millimeter of "additional" thinness. (Although it’s perfectly reasonable to argue that we’ve reached peak-thinness for the time being anyways.) The Pixel’s touchscreen is surprisingly useful and it happens more and more often that I reach for my Macbook’s display, especially when using Google Maps. I never expected this to happen when I made jokes about Microsoft’s attempts to establish touch on a desktop-OS.

![Chromebook Pixel side #1](/content/images/2014/Feb/IMG_20140220_014534.jpg)

The only weakness I could find so far is the back plate of the Pixel, which is a thin layer of aluminum that bends easily. Unfortunately, the previous owner managed to put a tiny dent into it while removing it in order to replace the LTE-modem with one which works within the EU. However, the device is easier to disassemble than the non-unibody Macbook Pro. If you ever had to open a non-Unibody Macbook, you will appreciate this.

## The Software

Let me say it bluntly: Chrome OS is the first Linux-distribution that just worked out of the box. There is zero input-lag, the trackpad works with amazing precision, the scrolling is perfectly fluid I have never seen Chrome *this* fast. It’s also the first time I’ve been blown away by the quality of Linux’ font-rendering. As far as I have learned, Chrome OS is using its own Aura-window manager, while X11 is simply a means to handle the hardware-input. Sadly, Chrome OS is pretty much unusable out of the box, if you want to do anything that cannot be done outside of the browser. I am one of these persons. I am a systems administrator which makes me pretty dependent on a shell and the dumbed down command line interface (ctrl+alt+t) just didn’t do it for me. Thanks to the fine people developing Chrome OS, Chromebooks are all setup to be configured to be put into a developer mode in which basically all codesigning is being stripped from the OS, while enabling access to a real Linux-shell (by typing shell into the basic Chrome OS-shell) - including the ability to gain root privileges via sudo. Basically, you are now running a heavily customized Gentoo-distribution on your Pixel. Just make sure to set a password for the chronos-account, unless you want everyone to get local shell access to your box via VT2. More on this is documented in the excellent [Chrome OS-wiki](http://www.chromium.org/chromium-os/poking-around-your-chrome-os-device). After being able to sudo, I chose to setup a separate chroot-environment with [crouton](https://github.com/dnschneid/crouton), to make sure that updates to Chrome OS’ base-system do not interfere with my customized setup.

![Chromebook Pixel side #2](/content/images/2014/Feb/IMG_20140220_014324.jpg)

I have settled with a with applications that are absolutely necessary for me, if I want to use this device in my free time. Most of these are the bare minimum to get anything useful out of Chrome OS.

* [TweetDeck](https://chrome.google.com/webstore/detail/tweetdeck-by-twitter/hbdpomandigafcibbmofojjchbcdagbl) is such an amazing client that it replaced Tweetbot for Mac on my Macbook Pro
* [Crosh Window](https://chrome.google.com/webstore/detail/crosh-window/nhbmpbdladcchdhkemlojfjdknjadhmh) is a simple wrapper that puts a terminal emulator into a basic window that doesn’t solely exist in a Chrome-tab
* [Google Drive](https://chrome.google.com/webstore/detail/google-drive/apdfllckaahabafndbhieahigkjlhalf) is where I keep most of my “not so private stuff” that I am comfortable enough to host in the cloud
* [Caret](https://chrome.google.com/webstore/detail/caret/fljalecfjciodhpcledpamjachpmelml) is a text-editor that has the option to be used with vim-shortcuts
* [Pixlr Touchup](https://chrome.google.com/webstore/detail/pixlr-touch-up/jklljiahjgoglchglekebfljnmbaleig) enables basic picture editing (though I’d give an organ or two for something as powerful as Pixelmator on Chrome OS)
* [500px](https://chrome.google.com/webstore/detail/500px/egpociadnldbkfkjpmjoaibnbcoeplja?hl=en) is a service I don’t really use myself but sometimes I just scroll through a few pictures to remind myself of the great display the Pixel has to offer





