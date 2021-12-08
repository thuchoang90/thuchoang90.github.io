---
layout: post
title: "FIC application: auto-exposure histogram equalization camera"
categories: Project
tags: Image-Processing
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

[Cyc5SoC_MTLC](/assets/sources/FICVideo/Cyc5SoC_Camera_MTLC.rar)

[DE2_115_MTLC](/assets/sources/FICVideo/DE2_115_Camera_MTLC.rar)

[DE2_115_VGA](/assets/sources/FICVideo/DE2_115_Camera_VGA.rar)

[SoCKit_MTLC](/assets/sources/FICVideo/SoCKit_Camera_MTLC.rar)

[SoCKit_VGA](/assets/sources/FICVideo/SoCKit_Camera_VGA.rar)

[SoCKit_VGA_HD.rar](/assets/sources/FICVideo/SoCKit_Camera_VGA_HD.rar)

[SoCKit_VGA_HD_HEdisplay](/assets/sources/FICVideo/SoCKit_Camera_VGA_HD_HEdisplay.rar)

[SoCKit_VGA_HD_HEdisplay_autoExposure](/assets/sources/FICVideo/SoCKit_Camera_VGA_HD_HEdisplay_autoExposure.rar)

demo.jpg
demo_HD.jpg
demo_HD_HEdisplay.jpg
demo_HD_HEdisplay_autoExposure.jpg

## III. Demonstration

The following demo is done with ```SoCKit_VGA_HD_HEdisplay_autoExposure```. The setting for screen display is given as follows:
![](/assets/sources/FICVideo/MonitorDisplay.jpg)

The demonstration:
![](/assets/sources/FICVideo/video.jpg)
<div class="container">
  <iframe src="https://www.youtube.com/embed/vkjfccmxcKw?autoplay=1&loop=1&mute=1" frameborder="0" allowfullscreen class="video"></iframe>
</div>

## IV. Citation

If you use the sources from this page in your published work, please cite the following:

As plain text:

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
