---
layout: post
title: Pixelbook Impressions
date: 2017-11-29 21:30:00
---

In 2013, Google introduced the Chromebook Pixel. It was the first time I actually considered Chrome OS and I had an urge I hadn't felt since Apple introduced the first Intel MacBook Pro: I wanted this thing. I needed to have it. But it was way out of my budget at that time and I had just gotten the first 13" Retina MacBook Pro as my work laptop, so it seemed kind of stupid to buy it. Of course I bought one a few months later, which I then sold again, only to buy a new one about a year later. I've adapted to putting everything in Google Drive and doing most of my work on remote machines years ago, so going all-in on Chrome OS wasn't as big of a deal. All I need for most of my work is an internet connection, a SSH client and a browser. The Chromebook Pixel aged quite well. Even compared to the new 2016 Macbook Pro, the Pixel felt sturdier and was still nicer to look at. But it didn't support Android apps and the battery left to be desired as well.

So, of course I had to buy the Pixelbook.

## Hardware 
The packaging it came in was weird. When you first hold the box the Pixelbook comes in, you might question if this device is actually as light as advertised on the spec sheet. But as soon as you take it out of the box, you'll be amazed at how light this thing is. I put it on my kitchen scale and it weighs 1119g or 1,1kg, as advertised. My Pixel C combined with the keyboard comes in at 909g but at a noticeably smaller form factor.

## Pixel Pen
The pen is pretty nice and there is close to no noticeable latency if the app supports it. But many don't. Those that do are awesome though. It's perfect for quick scribbles, even while the device is locked: You can open a drawing app like Google Keep on the lockscreen but you can change this to any other supported drawing app. Apps that aren't supported yet aren't working that well. The input of the pen lags and drawing or writing is no fun. [Evernote was pretty quick](https://blog.evernote.com/blog/2017/10/31/whats-new-evernote-pixelbook/) with their support for the Pen, so I'm confident others will follow suit.

I miss having a way to attach the pen to the device though. This way it's mostly resting in my backpack and it keeps on rolling away, when I'm putting it on a desk or if I'm sketching something on the couch.

## The Keyboard
The Keyboard is best in class, it's way ahead of the new MacBook Pro keyboard. The keys have travel but not too much. They make a really nice sound when clicked. They won't annoy your colleagues in the office, promise. The backlight is pretty nice and it gets really bright. 

## Android apps 
Telegram is a bit better as a Chrome app than the Android version, but mostly because the latter doesn't go to tablet mode when resized or fullscreened, which is weird. One of the nicer Android tablet apps actually looks like a stretched out phone app on a 12" display. There is some undeniable irony there. I'll keep on using the webapp for now.

In order to edit photos on Google Photos in Snapseed, Googles image editor, I had to install the Google Photos app from the Play Store. I have no idea why such a core product like Photos isn't fully integrated into the OS. This is such a wasted opportunity. Chrome OS ships with a beautiful picture viewer app and I have no idea why this app isn't used to put Google Photos front and center. Okay, so much for that short rant. Back to Android apps.

I can now finally control my Sonos rooms from a Chromebook. Thats something I really missed before. 

Because the Twitter browser app is a piece of shit, I'm using the Android version, though it isn't behaving as well as I hoped. It doesn't support any keyboard shortcuts and it forces you to constantly use the pointer to reach for the post-button. There isn't much to like about Twitter anyways.

Being able to run apps like Seriesguide on my laptop is quite nice.

Instagram behaves really strange: Clicking Instagram-links in Chrome opens the Android app, but profiles are strangely displayed inside the in-app browser of the Instagram app. Errr, what. I also can't scroll the image stream with the touchpad, if the pointer is above an image. If I move it to some of the whitespace, I can scroll again. I'm sure Instagram's multi-platform UI is to fault for that.

While I understand the rationale behind freezing Android apps as soon as they lose focus, I'm not convinced that's a nice user experience. Maybe keep them running for a few seconds with some kind of graphical feedback to indicate that the app won't run anymore?

For a brief history of how Android apps ended up on Chrome OS, read my piece on [Google's hardware strategy](https://blog.dictvm.org/google-hardware-strategy/). 

## Google Assistant
Having a dedicated button for the Assistant is awesome, especially since it defaults to keyboard input. 

Setting a timer doesn't work, it only opens the Play Store with the Clock app. If you then install the Clock app and give it another try, it just opens the Play Store again. The assistant still confirms that a timer has been set.  

## Tablet experience
I'm not sure I like the tablet mode. The Pixelbook is really big and the huge borders around the display aren't making things better. Because you can't separate the keyboard, it's also heavy to hold for long periods of time. Hell, even short periods are annoying. The Pixel density of the display is not that great either, if you plan on putting it in front of your nose. It's a bit worse than the 10" iPad Pro, which I [returned this summer](https://blog.dictvm.org/ipad-pro-return/), in part because of the low PPI. It's perfect for a laptop though. I'd rather have 10 hours of battery than the higher resolution.

I think I'll keep the Pixel C around for casual stuff on the couch. I just wont be needing the Pixel C's keyboard any longer, though it served me well for the last 2 years.

It is quite clear that Google isn't finished with their tablet optimizations for Chrome OS, considering that they just [added split screen](http://www.androidpolice.com/2017/11/11/google-adds-split-screen-snapping-chrome-os-tablet-mode/). I hope there's more to come in that area.

I tend to read a lot and I've noticed that I just put the Pixelbook in tablet mode to read something instead of just sending it to Pocket, to read it later. Chrome OS is really good as switching between the tablet- and laptop-mode, so the process of just folding it over to read something and go back to where I was, is a breeze.

## Tent Mode
Tent mode is surprisingly useful. I'll probably love it even more when travelling. I prefer the mode where I use the keyboard-base as a kickstand for the display a bit more though, because the rubber pads keep it more stable on the desk.

## Performance
Chrome performs like I've never seen it perform before. It's blazingly fast. It never ever stutters once, no matter what I throw at it.

Android apps start really quickly, though the Android runtime needs a few seconds until it fully loaded after a reboot.

## Annoyances 
On the prime platform for Chrome, the browser doesn't come with tap-to-zoom on devices that feature touchscreens. You have to manually pinch-to-zoom a specific text so it better fits the screen. And when you're scrolling while you're reading, prepare to be annoyed again: While scrolling, the text will shift a bit to the left and right, depending on your fingers' positions on the touchpad. I've actually [opened a bug report](https://bugs.chromium.org/p/chromium/issues/detail?id=632043) for that some months ago. Please star it, if you agree that this should be implemented.

## Productivity
What annoys me the most about Chrome OS is the fact that it lacks support for multiple workspaces. Considering how many engineers work at Google, it is strange that Chrome OS does not support this. According to this [feature request](https://bugs.chromium.org/p/chromium/issues/detail?id=309256), it requires some fundamental work to get this to work. There is a [follow-up to that](https://bugs.chromium.org/p/chromium/issues/detail?id=629871) though, that has been assigned to an engineer a few days ago. Make sure to star this as well, if you want to keep track of the progress.

## Development environment
Local development with a text editor is fine with Termux, while I'm bouncing between the Mosh Chrome Extension and Termius to do any work via SSH on remote servers. I try to keep most of my stuff on a server though. The local environment is for situations where I'm on really shitty connections. 

There is no support for Android Studio either and that sucks big time. I was just getting started to to build a prototype app using Flutter, but without an IDE on my main computer that's no longer that interesting.

If you need an IDE, don't buy the Pixelbook. Of course there's [developer mode](https://www.theverge.com/2017/11/16/16656420/google-pixelbook-chromebook-development-linux-crouton-how-to), but seriously, why not get a Macbook or Surface instead? 

## Roundup
All in all, I'm pretty happy with the purchase. It's a lightweight device, it can handle a lot of my productivity requirements, the display is bright and the Android app support is on route to becoming the missing piece to make Chrome OS more interesting for everyday productivity tasks. Of course there are still lots of reasons for people to not buy this thing, but for me, it's perfect.
