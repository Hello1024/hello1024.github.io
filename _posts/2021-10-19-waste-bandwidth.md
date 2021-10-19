---
layout: post
title: Visit this page to waste some bandwidth
---


Just sit on this page to waste bandwidth.

Bandwidth wasted:  <b><span id=bwused></span> megabytes.</b>

<script>
  function nextImage() {
    var a = (new Image());
    a.src="https://explorermarine.co.uk/1mb.jpg?foo="+Math.random();
    a.onload = () => window.nextImage();
    window.bwused.innerText = parseFloat(window.bwused.innerText)+1;
  }
  nextImage();
</script>
