---
layout: default
title: Blogs
---

<div style="padding:20px;border-style: dotted;">
  <h1><span style="#F6DDCC "> Midway through GSoC'22 </span></h1>
</div>


# <span style="color:#5DADE2"> Introduction </span>

Hello there, I am Rishikesh Donadkar. I am a Third Year B.tech student at Veermata Jijabai Technological Institute, Matunga, Mumbai. For the past 9 weeks I have been working as a GSoC Contributor in libcamera. The first 3 weeks were the community bonding period and following 6 weeks were the coding period.


# <span style="color:#5DADE2"> What is Libcamera? </span>

Libcamera is a camera support library supported on Linux, Android, Chrome OS. Libcamera exposes API that helps the Camera applications interact with the camera and provides various other features like
Device enumeration, Capabilities enumeration, Multi stream support, Controlling the stream on per-frame basis and a lot more.

# <span style="color:#5DADE2"> Project - Improve GStreamer element to add support for properties </span>

Libcameras offers a source element in the GStreamer pipeline.The GStreamer element allows libcamera to be used as a video source in the GStreamer pipeline. 


<div style="background-color:#566573;padding:20px;border-style: dotted">
  <h2>Short introduction about GStreamer.</h2>
    GStreamer is a pipeline-based multimedia framework that links together a wide variety of media processing systems to complete complex workflows. Pipelines are formed by linking elements with each other and the interface through which the elements are linked are called pads. Pad exposes certain capabilities, these capabilities describe the data that can flow or currently flows through the pad. A pad does a Caps query on its peer pads to know about the supported GstCaps, this is how the adequate format for dataflow within a GStreamer pipeline is decided through negotiation.
</div>
<br>

The aim of this project is to add support to the libcamera gstreamer element so that more aspects of the stream like the colorimetry, framerate can be controlled. Having this support will help configure the stream in the way the downstream element in the gstreamer pipeline requests or prefers.

# <span style="color:#5DADE2"> My experience as a GSoC contributor in libcamera </span>

This is the first time I am contributing to an open source project. Like most of the people who are new to the open source world I was intimidated by the huge codebase of libcamera. Like all other GStreamer elements libcamerasrc uses the <span style="color:#9CF110 "> GObject </span> programming model along with <span style="color:#9CF110 "> GLib </span>.
At first I found it quite difficult to study the code base. I learned how object orientation is done in using the GObject, following this I studied how the libcamera gstreamer element uses the GObject and GLib along with the libcamera exposed API to make a source element in the gstreamer pipeline. After understanding what all the functions do by looking at the  GStreamer upstream documentation, GObject and GLib documentation for API reference I got a clear picture of the code base. My mentors Umang and Vedant helped me a lot in understanding the code base and clearing the doubts I had.


## <span style="color:#C39BD3 "> Student Application period </span>
Most of the time in the student application period was spent on doing the warmup tasks. This was my first major encounter with the huge codebase of an open source project. I learned many things over this period like sending patches over email, studying large codebases and communicating effectively on the IRC and mailing-list.

The blog dedicated for the pre-gsoc selection can be found [here](https://rishi27-dot.github.io/gsoc/selection_prep/).

## <span style="color:#C39BD3 "> The Coding Period </span>
The coding period for GSoC’22 started on 12th of June. There were many aspects of the stream that could be controlled. Two major properties that needed support in the libcamera gstreamer element are colorimetry and framerate. Umang suggested that we must first work with the colorimetry as that was relatively easy and straight forward than the framerate. I made an action plan for adding the colorimetry support and shared it with the mentors. After getting the approval form Umang I started coding.  Every week I used to have a weekly sync meeting with the mentors to share the progress, clear the blockers and list down the pending actions. I logged the progress in the community bonding period and Coding period in the Progress Tracker.

[Progress Tracker](https://rishi27-dot.github.io/gsoc/home/)

### <span style="color:#F1948A "> Colorimetry Support </span>

In the GStreamer colorimetry consist of four fields namely primaries, color matrix, transfer function and range. GStreamer elements negotiate colorimetry in the form of strings through the capabilities. A downstream element will request single or multiple colorimetry through the caps and libcamera will provide a stream with the requested colorimetry if it can be supported by the camera hardware. Following examples show how colorimetry can be requested in the GStreamer pipeline using [capsfilter](https://gstreamer.freedesktop.org/documentation/coreelements/capsfilter.html?gi-language=c).

Single colorimetry
```
gst-launch-1.0 libcamerasrc ! video/x-raw,colorimetry=bt709 ! ...

```
In this case, the colorimetry requested is parsed and converted to a GstVideoColorimetry and the fields of this struct like range, matrix, transfer, primaries are mapped to the to the Range, YcbcrEncoding, TransferFunction, Primaries of the <span style="color:#F9E79F "> libcamera::ColorSpace </span> class.
The ColorSpace obtained as a result of this conversion is tried on the sensor and if the sensor supports this kind of ColorSpace then the camera can be configured to produce stream(s) with the requested colorimetry.

Multiple colorimetry
```
gst-launch-1.0 libcamerasrc ! "video/x-raw,colorimetry={bt709,bt2020}" ! ...

```
In this case the multiple colorimetry options are requested in preference order , any one among these colorimetreis if supported by the camera hardware is chosen and applied to the stream(s).

Downstream elements can also specify the colorimetry they prefer/want through the caps exposed on their sink pad.

# <span style="color:#5DADE2"> Ongoing work </span>

* Testing single colorimetry support.
* Multiple colorimetry support.
* Framerate negotiation support.

# <span style="color:#5DADE2"> Summary </span>

I would like to thank Google Summer of Code and libcamera for giving me this opportunity to contribute to the open source community. I have learned a lot of new things and boosted my skills in the GSoC journey so far and I hope to learn more.
