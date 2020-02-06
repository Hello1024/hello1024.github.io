---
layout: post
title: The browser memory feast
---

I've been looking for a really good browser - problem is I can't find one.

They all suffer from a common problem - when you open up too many tabs and windows, they get slow, the system gets slow, and switching tabs and loading pages takes forever.

How can we fix this?  My initial thought is hat there is no reason for non-active tabs to be kept in memory.  I mean we could just unload the tab and all it's contents, just remembering the URL it was showing.  When the user wants to go back to that tab we simply re-load the page.

There are two problems with this though:
<ol><li> It's slow - can you imaging having to wait for the page to reload every time you wanted to change tabs?</li>
<li>It would break some websites - Many websites, for example bank websites don't allow page refreshes, and if they do they inconviently redirect you to another page.  Consider for example gmail, where if you refresh the view sometimes changes.</li></ol>

A better solution would be to somehow serialize the contents of the whole page - effectively take the whole DOM tree and all the JavaScript objects and pack them into a single data stream and save that on disk somewhere.  Then you could shut down the whole render process.  When you want to view the tab again you simply deserialize the DOM tree and re-render it.

But wouldn't that serialised version take up just as much memory?  Well theoretically, yes, but practically no.  There are lots of buffers and caches inside a renderer that wouldn't be kept inside the serialised version of a page.  Also, generally the renderer keeps an uncompressed bitmap copy of the whole page and every constituant image, whereas the serialized version could just keep the original image (as downloaded from the server), which would be much smaller.

By a quick calculation, this means that size of the serialized version of most pages need not be bigger than approximately the downloaded size of the page, plus the size of any javascript objects, and a tiny amount for any state. (I assume a serialized DOM won't be much bigger than an HTML file - I mean the HTML file describes the initial state of the DOM anyway).  This means for most pages, we could probably have an entire page stored inside 500kb.

So what about speed?  Well the time to serialize a page isn't really relevant, because it can happen in the background.  The time to deserialize a page is important though.  Since the file format for the serialized page isn't very important, we can tailor the format to keep information that is CPU intensive to recalculate, like the exact positioning of elements, clipping regions, and layering information.  Considering that, when the DOM is loaded into memory, I can't see why showing it would take more than about half the time of rendering a file from plain, local HTML files. (the speedup is due to the fact all the resources required are already in memory rather than on disk with latency, and all the CPU intensive layout operations have already been done, and there is no Javascript to execute).

So how long will it take to change tabs?  Currently in a browser like chrome, changing tabs is seemingly instant (<100ms) for recent tabs, and about 5 seconds for tabs that have been open in the background for days, and therefore paged to disk.  There isn't much improvement we can make on the "instant" ones, but the 5 second ones we can certainly improve.  If, when switching tab we load in a 500kb serialized page (say that takes 15ms), and take half the normal time to render it (500ms), we have a fully rendered page inside 515ms.  The 500ms portion of this could probably be significantly reduced by saving the right data in the serialized page, possibly down to 100ms.

But, even so, I don't want to wait 515ms to change tabs!  The next speedup is that we could store a screenshot of the page within the serialized version of a page.  I have found that a low quality 50kb JPEG screenshot provides a suitable preview-quality image.  This could be saved together with the serialized page.  When the user clicks the tab, first show the "preview" image, and then load and unserialize the page - now total time to display something is more like 25ms (15ms to load that serialized data, and ~10ms to decode the screenshot), which is well below what humans perceive as instant.  The full page would then proceed to load in the background for up to 500ms, which is about the time the user would take to begin interacting with the page anyway.

So how could the above help?  Well now the number of "open" pages is in no way related to available memory, so we could have thousands of open pages without any slowdown.  But why?  Consider for a moment, why do you ever close a page?  Probably to free up space on the tab bar or to help organise things.  If however a better tab bar could be designed which was fully integrated into the history function, such that you never needed to close anything, they just faded into history, and you could retrieve them from history and they'd still be open and active.

Now there is no need to ever close a tab, ever.  Everything can stay open, even through a reboot.  You would be able to flick though anything in history - never mind if it's something you were looking at 30 seconds ago or something you haven't looked at for months, and you would be guaranteed to be able to view the page within 25ms and interact with it before you can get your mouse into the frame.

From a technical standpoint, there are really 3 states a page could be in:
<ol><li>In memory, rendered - for a tab thats currently showing</li>
<li>Serialized In memory - for a tab thats has been showing within the last few minutes, so it can be loaded without hard disk access</li>
<li>Serialized on disk - for a tab that hasn't been used for a few minutes - it now isn't using any of those precious resources</li></ol>

There are disadvantages with what I've described.  The issues are mainly related to plugins - using current API's, no plugins can serialize themselves, and therefore the plugin would have to be re-loaded when the page is reshown.  That means for example, Youtube videos would end up at the start again.  It could also break some sites where the plugin communicates with the javascript of the page.  This won't be much of a problem in the future because more and more sites will hopefully move to html5 video and less flash, and also, if a major browser implements the above, plugin makers will add saving and restoring state to their own codebases.

The next problem is pages which interact even when in the background.  Consider for example a page with a websocket or pending HTTP request or running timer, such as a chat program or music player.  When it's serialized, all events would have to be queued up for when the page is re-activated.  The only solution for this is detecting these cases and not serializing them for more time, and when they are serialized, have some event that fires so the page can, if it chooses to, reconnect whatever websockets it was using.

The advantages of the above, such as not having to wait a long time to switch tabs and being limited to not many tabs, certainly outweigh the effort to add this feature and the few possible compatibility problems it could cause.  Unfortunately, I think this project is too big for me, or I would have tried to implement it in one of todays open browsers, which is why I write about it here in the hope someone can take and extend my ideas and implement them one day!
