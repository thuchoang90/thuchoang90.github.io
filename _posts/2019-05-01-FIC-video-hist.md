---
layout: post
title: "FIC application: auto-exposure histogram equalization camera"
categories: Project
tags: Image-Processing FPGA
---
<style>
  .container {
    position: relative;
    width: 100%;
    height: 0;
    padding-bottom: 56.25%;
  }
  .video {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
  }
</style>

## I. Histogram Equalization (HE) & Matlab source

Histogram equalization is a method for modifying the image based on its histogram. The primary purpose is for contrast enhancement. Please read the following paper for details about the algorithm: "A Histogram Modification Framework and Its Application for Image Contrast Enhancement" [[DOI]](https://doi.org/10.1109/TIP.2009.2021548).

The idea of HE is to create a function that makes the dark pixels a bit brighter and the bright pixels a bit darker, thus stretching out, or balancing out, the histogram. For this project, we prepared a Matlab source for HE demonstration: [download](/assets/sources/FICVideo/Matlab.rar). To run the demo, first open your Matlab, then go to the ```Matlab/src/``` folder and you'll see the ```BasicHE.m``` file. Executing by: ```BasicHE(<image path>)```; for example: ```BasicHE('Standard Test Images\misc\4.1.01.tiff')``` and you'll get this result:
![](/assets/sources/FICVideo/ex.jpg)

## II. FPGA sources

Several FPGA demos are prepared. And they are given with some options as follows.

### II. a) Display using on-board LCD

![](/assets/sources/FICVideo/demo.jpg)

These FPGA demos using on-board LCD to display the video. The available sources are:
  - Cyclone V SoC: [Cyc5SoC_Camera_MTLC.rar](/assets/sources/FICVideo/Cyc5SoC_Camera_MTLC.rar)
  - DE2-115: [DE2_115_Camera_MTLC.rar](/assets/sources/FICVideo/DE2_115_Camera_MTLC.rar)
  - Arrow SoCKit: [SoCKit_Camera_MTLC.rar](/assets/sources/FICVideo/SoCKit_Camera_MTLC.rar)

### II. b) Display using VGA

![](/assets/sources/FICVideo/demo_HD.jpg){:height="75%" width="75%"}

These FPGA demos using VGA to display the video. The available sources are:
  - DE2-115:            [DE2_115_Camera_VGA.rar](/assets/sources/FICVideo/DE2_115_Camera_VGA.rar)
  - Arrow SoCKit:       [SoCKit_Camera_VGA.rar](/assets/sources/FICVideo/SoCKit_Camera_VGA.rar)
  - Arrow SoCKit (HD):  [SoCKit_Camera_VGA_HD.rar](/assets/sources/FICVideo/SoCKit_Camera_VGA_HD.rar)

### II. c) Display using VGA, with HE

![](/assets/sources/FICVideo/demo_HD_HEdisplay.jpg){:height="75%" width="75%"}

This FPGA demo is similar to the previous sub-section's ```Arrow SoCKit (HD)```. The only difference is that the HE is displayed on the same monitor together with the video stream.
  - Arrow SoCKit (HE): [SoCKit_Camera_VGA_HD_HEdisplay.rar](/assets/sources/FICVideo/SoCKit_Camera_VGA_HD_HEdisplay.rar)

### II. d) Display using VGA, with HE and auto-exposure

![](/assets/sources/FICVideo/demo_HD_HEdisplay_autoExposure.jpg)

This FPGA demo is similar to the previous sub-section's ```Arrow SoCKit (HE)```. The only difference is that now it has the feature of auto-exposure feeding back to the camera.
  - Arrow SoCKit (HE & auto-exposure): [SoCKit_Camera_VGA_HD_HEdisplay_autoExposure.rar](/assets/sources/FICVideo/SoCKit_Camera_VGA_HD_HEdisplay_autoExposure.rar)

## III. Demonstration

The following demo is done with the ```SoCKit_Camera_VGA_HD_HEdisplay_autoExposure.rar```. The setting for screen display is given as follows:
![](/assets/sources/FICVideo/MonitorDisplay.jpg){:height="50%" width="50%"}

The demonstration:
![](/assets/sources/FICVideo/video.jpg)
<div class="container">
  <iframe src="https://www.youtube.com/embed/vkjfccmxcKw?autoplay=1&loop=1&mute=1" frameborder="0" allowfullscreen class="video"></iframe>
</div>

## IV. Citation

If you use the sources from this page in your published work, please cite the following. As plain text:

```Takahiro Hosaka, Trong-Thuc Hoang, Van-Phuc Hoang, Duc-Hung Le, Katsumi Inoue, and Cong-Kha Pham, "Live Demonstration: Real-time Auto-exposure Histogram Equalization Video-system Using Frequent Items Counter," in Proc. of IEEE Int. Symp. on Circ. and Syst. (ISCAS), Sapporo, Japan, May 2019, pp. 1-1.```

As bib-entry:
```{% raw %}
@inproceedings{HosakaFIC2019,
  author    = {{Takahiro Hosaka, Trong-Thuc Hoang, Van-Phuc Hoang, Duc-Hung Le, Katsumi Inoue, and Cong-Kha Pham}},
  title     = {{Live Demonstration: Real-time Auto-exposure Histogram Equalization Video-system Using Frequent Items Counter}},
  booktitle = {{IEEE Int. Symp. on Circ. and Syst. (ISCAS)}},
  address   = {{Sapporo, Japan}},
  year      = {{May 2019}},
  pages     = {1--1}
}
```{% endraw %}
