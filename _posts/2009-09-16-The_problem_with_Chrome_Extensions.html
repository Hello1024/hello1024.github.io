---
layout: post
title: The problem with Chrome Extensions
---

One big aim for Extensions in any browser is to provide something which modifies the page the user is viewing.  For example, one might want to highlight certain links, add spellcheck, block flash, block ads, or implement parental controls.

The "content scripts" part of Googles extension system is designed specifically for this, but there is one large flaw - A content script can't modify page content on the fly as it's loaded.

For example, if you wanted to make a content script that removes all images from the page, you would have to wait until after the image is already on the page, and then remove it from the page.  The problem with that is that in the short amount of time the image is there, it will start loading.  Therefore if your aim is to remove images to reduce the network bandwidth (eg. for mobile internet), then that approach is useless.

The same applies for adblock - the best adblock you can currently implement is one that removes the ads after they've already started loading.  In the case of flash ads, this means that the flash plugin has already been fired up, and consumed lots of CPU time and delayed the page load.

The main reason I want adblock/flashblock for Chrome is to keep it fast even on those sites with lots of animated ads - having a crippled extension system like this allows me to block ads, but not solve the underlying slowness they cause.

From a technical standpoint all the chrome developers need to do is implement a few more events for content scripts - for example one which allows parts of downloaded HTML to be parsed and modified before it gets rendered, or alternatively some "onBeforeDOMNodeAdded" event.  The problem with both of these approaches is it would be possible for a slow addon to delay the page load, and Google is trying to avoid that at all costs.
