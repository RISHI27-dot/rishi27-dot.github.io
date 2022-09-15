---
layout: default
title: Final Report
---

<div style="background-color:#566573;padding:20px;border-style: dotted; text-align: center; font-size: 32px;">
Google Summer Of Code 2022 Final Report
</div>
<br>

This is Google Summer of Code 2022 project under libcamera aimed at adding support for the following:

* Adding colorimetry support to libcamera's GStreamer source element.
* Adding framerate control and negotiation support to libcamera's GStreamer source element.

## <span style="color:#98D435"> Project Details </span>
<hr>
<span style="color:#07E5EC"> Contributor Name:</span> Rishikesh Donadkar
<hr>
<span style="color:#07E5EC"> Mentors:</span> Vedant Paranjape, uajain
<hr>
<span style="color:#07E5EC"> Organization:</span> libcamera 
<hr>

<span style="color:#07E5EC"> Project:</span> Improve GStreamer element to add support for properties
<hr>

<span style="color:#07E5EC"> Links:</span>
* [Code](https://git.libcamera.org/libcamera/libcamera.git/)
* [Project Page](https://summerofcode.withgoogle.com/programs/2022/projects/WyqdLcia)  
* [Progress Log](/gsoc/home)  
* [Midway blog](/midway_blog/home)  
<hr>

## <span style="color:#98D435"> Overview </span>

Gstreamer is a pipeline based flexible and extensible multimedia framework. Libcamera offers a source element (libcamerasrc) for the GStreamer pipeline. The aim of this gsoc project is to add support for framerate and colorimetry to libcamera's gstreamer element.

In Gstreamer pipeline different elements are linked to each other and negotiate and decide on formats of the data that will flow through the pipeline. This is done through capabilities negotiation. Downstream suggests formats and the upstream element decides on the format that it can offer.  

## <span style="color:#C39BD3 "> Adding colorimetry support to libcamera's GStreamer source element. </span>
Colorimetry consists of 4 parameters namely primaries, transfer function, color matrix and range. With colorimetry support libcamerasrc can negotiate the colorimetry with the peer elements. Appropriate colorimetry is decided in the libcamerasrc by mapping the four identifiers of ColorSpace to the corresponding identifiers in GStreamer and deciding on appropriate ColorSpace corresponding to the colorimetry requested by the neighbouring element in the gstreamer pipeline.

The following colorimetry negotiation support was added to libcamerasrc. 
### <span style="color:#F1948A "> Single Colorimetry Support </span>

The neighbouring element requests the colorimetry it wants/prefers by exposing it on its pads, libcamerasrc decides on the colorimetry. This patch adds support to work with single colorimetry.

<span style="color:#FC0575 ">To test single colorimetry example using caps filter:</span>

```
gst-launch-1.0 libcamerasrc ! video/x-raw,colorimetry=bt709 ! glimagesink
```
### <span style="color:#F1948A "> Multiple Colorimetry Support </span>

Elements can also suggest multiple colorimetry on its pads. With this functionality libcamerasrc can negotiate and choose the best colorimetry for the stream. Downstream element will suggest the colorimetries on its pad and libcamerasrc will decide on one of the colorimetry from the suggestions.

<span style="color:#FC0575 ">To test multiple colorimetry using caps filter: </span>
```
gst-launch-1.0 libcamerasrc ! "video/x-raw,colorimetry={bt2020,bt709,sRGB}" ! glimagesink
```
## <span style="color:#C39BD3 "> Adding framerate control and negotiation support to libcamera's GStreamer source element. </span>

With this functionality libcamerasrc can control and negotiate framerate of the stream.

<span style="color:#FC0575 ">To test multiple colorimetry example using caps filter: </span>
```
gst-launch-1.0 libcamerasrc ! video/x-raw,framerate=30/1 ! glimagesink
```
## <span style="color:#98D435"> Contributions </span>

1. [Provide colorimetry <> ColorSpace mappings](https://git.libcamera.org/libcamera/libcamera.git/commit/?id=fc9783acc6083a59fae8bca1ce49635e59afa355)

2. [Provide multiple colorimetry support](https://patchwork.libcamera.org/patch/17174/)

3. [Provide framerate support for libcamerasrc](https://patchwork.libcamera.org/patch/17370/)

## <span style="color:#98D435"> Conclusion </span>
I am very grateful to Google Summer Of Code and Libcamera for giving me this opportunity to contribute to the open source community. I have learned a lot of things that will help me in my future endeavors. It was a great experience working with libcamera. I would like to thank my mentors Vedant and Umang for helping me out whenever I was stuck. I would also like to thank other members of libcamera organization for participating in the discussion and helping me. I will continue to work on this project and contribute in solving bugs, testing and implementing additional features if required.