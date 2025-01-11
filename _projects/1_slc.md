---
layout: page
title: structured light camera
description: my capstone project at OSU
img: assets/img/1_cupScan.jpg
importance: 1
category: 
related_publications: true
---

This is easily one of my favorite projects I've worked on. It combines computer vision algorithms with web development and microcomputer programming in a way that produces a dazzling spectacle of a result - this result being a 3D representation of a real-world object!
My experience with computer vision before starting this project was shaky at best. I couldn't tell you what the term "structured light" meant, nor how stereo vision works. I will go into more detail as to what these mean, and how these concepts come together to create a system capable of synthesizing 3-dimensional objects.

To get started, I should explain *what* this project is.

## general setup
<div class="row">
  <div class="col-sm mt-3 mt-md-0">
    A structured light camera is a system consisting of a camera and a projector (like what you would find in a conference room). Using a controller computer, the system synchronizes the camera and projector in order to capture unique images of an object. This controller sends patterned images to the projector, then captures image input from the camera for each image. From these 2D images, the system uses some complex 3D linear algebra to estimate a 3rd dimension for each pixel.
  </div>
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid loading="eager" path="assets/img/1_cupScan.jpg" title="a cup being scanned" class="img-fluid rounded z-depth-1" %}
    <div class="caption">
      Caption photos easily. On the left, a road goes through a tunnel. Middle, leaves artistically fall in a hipster photoshoot. Right, in another hipster photoshoot, a lumberjack grasps a handful of pine needles.
    </div>
  </div>
</div>

## coordinate math
<div class="row">
  <div class="col-sm mt-3 mt-md-0">
    At its core, structured light is a problem of triangulation. We know the locations of two points: a pixel of the projected image, and a pixel of the image captured by the camera. Since the projector and camera are oriented at two different places in space, the pixels are points in different coordinate systems. This means that their positions are defined by terms. We can work around this by looking at the physical relationships between the camera and projector. These are mathematically defined by the extrinsic parameters, represented by the matrix **R** and the vector **t** in the image to the right.
    The vector **R** is known as the rotation matrix. This specifies the roll, pitch, and yaw rotations needed to map a projector coordinate to a camera coordinate. Applying these rotation transformations to one of the camera or projector results in both of these systems being parallel.
    The vector **t** is known as the translation vector. This specifies the distance and direction to move the camera or projector to the other. Applying the translation to one of these results in both of these systems being located at the same location.
  </div>
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid loading="eager" path="assets/img/1_triang.png" title="triangulation" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
So, using both the **R** and **t**, we can map points from one coordinate system into the other. Since we now know pairs of points within the same coordinate system, we can approach this as a triangulation problem as we originally intended.

## implementation
Now, for the iteration I worked on, we:
- Used a webcam and projector that one of us had lying around.
- Based our project around the OpenCV implementation of structured light.
- Implemented point cloud generation *and* mesh generation.
- Designed the system to be modular and user-friendly.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/1.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/3.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/5.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Caption photos easily. On the left, a road goes through a tunnel. Middle, leaves artistically fall in a hipster photoshoot. Right, in another hipster photoshoot, a lumberjack grasps a handful of pine needles.
</div>
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/5.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    This image can also have a caption. It's like magic.
</div>

You can also put regular text between your rows of images, even citations {% cite einstein1950meaning %}.
Say you wanted to write a bit about your project before you posted the rest of the images.
You describe how you toiled, sweated, _bled_ for your project, and then... you reveal its glory in the next row of images.

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/6.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/11.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    You can also have artistically styled 2/3 + 1/3 images, like these.
</div>

The code is simple.
Just wrap your images with `<div class="col-sm">` and place them inside `<div class="row">` (read more about the <a href="https://getbootstrap.com/docs/4.4/layout/grid/">Bootstrap Grid</a> system).
To make images responsive, add `img-fluid` class to each; for rounded corners and shadows use `rounded` and `z-depth-1` classes.
Here's the code for the last row of images above:

{% raw %}

```html
<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/6.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
  </div>
  <div class="col-sm-4 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/11.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
```

{% endraw %}
