---
layout: post
title: How much memory does the linux kernel waste?
---

How much RAM on your laptop is sitting unused?  How much is empty?  How much is redundant?

In an ideal OS, the answer is none.  All RAM contains data of running programs, or buffers or cache to help speed up things you're about to do.

But what about reality?   A quick [bit of python](https://gist.github.com/Hello1024/4902ff3bdba32a219adb4caa3563c23a) and
[a kernel module](https://github.com/Hello1024/devmem-full-access) later, and I now know!

System: Ubuntu 20.10 laptop, with 16 Gigs of RAM, running Chrome with +20 tabs, playing a bit of music and running a few other apps (Freecad, Deluge, Sublime).  Pretty typical desktop workload.


### Results...

Of my 15.7 Gigs of RAM...   2.05 Gigs are exact duplicates of other memory (1.1Gigs of that are zeros), and 13.6 Gigs are unique.

### How frequent are the duplicates?

![Frequency plot](/images/dupemem-freqplot.png)

### What data has the most duplicates?

The most common are all zeros, all `0xff`'s, all `0xcc`'s (used by some memory debuggers?), and various patterns that I suspect are freelists of various memory allocators.

### What is a typical duplicate?

Lets take a look at the 4k page of RAM with hash 0372a15ebe749b18d397c9dffdc55d21.  There are 5 copies of it.  The actual data is:

    gBFACQAJYAUgBUAC2AF4AYwA...lots more base64...A;gdpr=1;dc_adk=4100875739;ord=r2qk1l;click=https%3A%2F%2Fclicktrack.pubmatic.com%2FAdServer%2FAdDisplayTrackerSer

So it's a bit of a cookie.   Is it a good use of RAM to keep 5 copies?

### What about free memory

This system claims:
```
# free
              total        used        free      shared  buff/cache   available
Mem:       16153824     5098156     5662776      893616     5392892     9826072
```

Most of those 'free' pages contain data from previous programs, and is counted in the above analysis.   Quite why we have so much free memory when we could be preloading potentially useful data is another question...

### Conclusion

My RAM has a lot of duplicate data in.  This seems at odds with good design practices which should keep just one copy of big chunks of identical data.   Anyone fancy running the same code on their system, tracking down who is copying and allocating this data, and sending patches to the relevant projects to keep just one copy of this data and allow the RAM to be used for better things.
