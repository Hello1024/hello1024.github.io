---
layout: post
title: HTML Canvas - adding a dimension...
---

The web is such a great platform, but there are still things it can't do, and one of them is support for decent graphics without flash.  HTML 5, the next version of the html the web is written in, goes some way to address this.  With HTML5 you can do pretty much anything you like with 2D graphics by using the new &lt;CANVAS&gt; tag.

The problem is I hate limits, and therefore uncontent with my new 2D canvas, I want more!  So I've been fiddling with software 3D rendering inside javascript.

Here's my first attempt:  (note - this only works on the latest versions of Chrome, Opera, Firefox, or Safari)

<script>

// load a test image into the canvas given as a function parameter.
// the image is given by the hideous data url below.
  
function copyTestImageToCanvas(canvasA) {
  var imgA = document.getElementById('inimage');
  //imgA.src="";
  
  // use the smaller of the two dimensions
  var size=canvasA.width;
  if (canvasA.height<size) size=canvasA.height;
  
  canvasA.width=size;
  canvasA.height=size;

  canvasA.getContext("2d").drawImage(imgA,0,0);
}

// bodge to do animation... - it's unstoppable!
function animateStep(timer) {
  wrapHelper(  document.getElementById('cana'),
    document.getElementById('canb'),
    parseFloat(document.getElementById('scale').value),
    Math.sin(timer/100)*Math.PI/3,
    timer/20*Math.PI);
  setTimeout("animateStep("+(timer+1)+");", 20);
}

// a helper function to do all the data conversions etc.
function wrapHelper(canvasA, canvasB, scale, elevation, rotation) {

  var size=canvasA.width;
  
  // get the input image data
  var ctxA = canvasA.getContext("2d");
  var dataA = ctxA.getImageData(0,0,size,size);

  // make an array for output image data (same dimensions as inout)
  var ctxB = canvasB.getContext("2d");
  var dataB = ctxB.createImageData(size, size);
  
  // call our transformation function
  wrap(dataA, dataB, size, scale, elevation, rotation);

  // put the output back into the canvas
  ctxB.putImageData(dataB,0,0);

}

// helper function to copy a pixel from A to B using x,y coordinates in each.
function copyPixel(A, Ax, Ay, B, Bx, By){ 

  // round all the values to the nearest pixel
  Bx=Math.round(Bx);
  By=Math.round(By);
  Ax=Math.round(Ax);
  Ay=Math.round(Ay);
  
  // check it's within the area of both images
  if (Ax>0&&Ax<A.width&&Ay>0&&Ay<A.height&&Bx>0&&Bx<B.width&&By>0&&By<A.height) {
  
    // we need to copy Red, Green, Blue, and Alpha all together
    B.data[4*(By*B.width+Bx)+0] = A.data[4*(Ay*A.width+Ax)+0];
    B.data[4*(By*B.width+Bx)+1] = A.data[4*(Ay*A.width+Ax)+1];
    B.data[4*(By*B.width+Bx)+2] = A.data[4*(Ay*A.width+Ax)+2];
    B.data[4*(By*B.width+Bx)+3] = A.data[4*(Ay*A.width+Ax)+3];
  }
}
  
// do the actual trasformation - wrap the image in dataA onto dataB, given 
// the parameters shown
function wrap(dataA, dataB, size, scale, elevation, rotation) {

  //iterate through every point in the output image
  for (j=0; j<size; j=j+1) {
    for (i=0; i<size; i=i+1) {
    
      // i and j are the point on the output image
      // x and y are the point on the input image
    
      // calculate the equivilant point in the input image 
      
      // center about 0, and scale so radius is 1
      x=(i-size/2)*scale;
      y=(j-size/2)*scale;
      
      // calculate depth
      z=Math.sqrt(size*size/4-x*x-y*y);
      
      // check we're in the area
      if (!z) continue;
      
      // do a rotation in one direction (use Y and Z)
      newy = y*Math.cos(elevation) - z * Math.sin(elevation);
      z    = y*Math.sin(elevation) + z * Math.cos(elevation);
      
      // do a rotation in the other direction (use X and Z)
      newx = x*Math.cos(rotation) - z * Math.sin(rotation);
      z    = x*Math.sin(rotation) + z * Math.cos(rotation);
      
      // translate back to image coords, ignore z as a simple projection
      newx = newx+size/2;
      newy = newy+size/2;
      
      //copy from the input image to the output image.
      copyPixel(dataA, newx, newy, dataB, i, j);
    }
  }
}


</script>

<body onload="copyTestImageToCanvas(document.getElementById('cana'))">
<h1>3d ball test page</h1>
<p>Page where we aim to wrap image A below around a sphere and project it back 
   into image B using the settings below</p>
<FORM action="..." method="post">
<TABLE>
  <TR>
    <TD><LABEL for="scale">Scale Factor</LABEL>
    <TD><INPUT type="text" name="scalea" id="scale" value="1">
  <TR>
    <TD><LABEL for="elevation">Elevation</LABEL>
    <TD><INPUT type="text" name="elevationa" id="elevation" value="0.9">
  <TR>
    <TD><LABEL for="rotation">Rotation</LABEL>
    <TD><INPUT type="text" name="rotationa" id="rotation" value="0">
</TABLE>
<INPUT type="button" name="go" value="Go" onclick="wrapHelper(  document.getElementById('cana'),  document.getElementById('canb'),  parseFloat(document.getElementById('scale').value),  parseFloat(document.getElementById('elevation').value),  parseFloat(document.getElementById('rotation').value)  );" >
  
  <INPUT type="button" name="animate" value="Animate" onclick="animateStep(0);">
</FORM>
<p>The images</p>
<TABLE>
  <TR>
    <TD>Image A
    <TD>Image B
  <TR>
    <TD><CANVAS id="cana">
    <TD><CANVAS id="canb">
</table>
<img id="inimage" src="http://www.omattos.com/sites/default/files/test.gif" onload="copyTestImageToCanvas(document.getElementById('cana'));">
