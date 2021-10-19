---
layout: post
title: Visit this page to waste some bandwidth
---


Just sit on this page to waste bandwidth.

Bandwidth wasted:  <b><span id=bwused>0</span> megabytes.</b>

Rate of waste:  <b><span id=bwrate>0</span> Mbps.</b>


Close this window to stop wasting bandwidth.

<script>
  function nextImage() {
    var a = (new Image());
    a.src="https://explorermarine.co.uk/1mb.jpg?foo="+Math.random();
    a.onload = () => window.nextImage();
    imgcount = parseFloat(window.bwused.innerText);
    window.bwused.innerText = imgcount+1;
    window.bwrate.innerText = (imgcount*8e3/(Date.now()-startTime)).toPrecision(2);
  
  }
  startTime = Date.now();
  nextImage();nextImage();
</script>
