---
layout: post
title: Choppy Bluetooth Audio playback on macOS
date: '2016-08-18 17:05:30'
---

macOS has had some issues with Bluetooth Audio since the release of Yosemite. The symptom is that audio playback stutters while causing your other Bluetooth peripherals, like your Trackpad or keyboard, to lag or even lose their connection.

After reading [several suggestions](https://twitter.com/dictvm/status/766312167549308928) on how to fix these, I spend a few minutes of testing to find a configuration that works with a Bose SoundLink Mini 2 in a 30sqm office. I have found a mixture of values that work in an environment with crowded Bluetooth usage surrounded by lots of WiFi usage in the 2,4Ghz band. 

Please take [these values](https://gist.github.com/dictvm/85cc6ee19036ae292c0d1f2adcefd9bf) with a grain of salt. To be sure, use `defaults read com.apple.BluetoothAudioAgent  > bluetoothd-conf-current` to have a backup of your current settings.