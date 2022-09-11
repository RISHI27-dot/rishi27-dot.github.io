
This is Google Summer of Code 2022 project under libcamera aimed at adding support for the following:

* Adding colorimetry support to libcamera's GStreamer source element.
* Adding framerate control and negotiation support to libcamera's GStreamer source element.

## <span style="color:#98D435"> Project Details </span>
* Contributor Name: Rishikesh Donadkar
* Mentors: Vedant Paranjape, uajain
* Organization: libcamera
* [Code](https://git.libcamera.org/libcamera/libcamera.git/)
* [Project Page](https://summerofcode.withgoogle.com/programs/2022/projects/WyqdLcia)
* [Progress Log](/gsoc/home)
* [Midway blog](/midway_blog/home)

## <span style="color:#98D435"> Overview </span>

Gstreamer is a pipeline based flexible and extensible mulitmedia framework. Libcamera offers a source element(libcamerasrc) for the GStreamer pipeline. The aim of this gsoc project is to add support for framerate and coloriemtry to libcamera's gstreamer element.

In Gstreamer pipleline differenet elements are linked to each other and negotiate and decide of formats of the data that will flow through the pipeline. This is done through capablites negotiation. Downstream suggests formats and the upstreame element decides on format that it can offer. 

## <span style="color:#C39BD3 "> Adding colorimetry support to libcamera's GStreamer source element. </span>
 The following colorimmetry negotiation support were added to libcamerasrc.
### <span style="color:#F1948A "> Single Colorimetry Support </span>

Colorimetry consist of 4 parameters namely primaries, transfer function, color matrix and range. With this functionality libcamera can negotiate the colorimetry. Appropriate coloriemtry is decided in the libcamerasrc by mapping the four identifiers to the corresponding identifiers in libcamera and decide on apporprialte colorspace corresponding the the colorimetry requestd by the neighbouring element in the gstreamer pipeline. The neighbouring element request the colorimetry it wants/prefers by exposing it on its pads. This patch only works with single colorimetry negotiation.

Usage
```

```
### <span style="color:#F1948A "> Multiple Colorimetry Support </span>

Elements can also specifiy comma seprated list of colorimetry that it can work with and with this functionality libcamerasrc can negotiate the colorimetry list. Downstream element will suggest the colorimetries on its pad and libcamerasrc will decide on one of the coloriemtry from the suggestions.

Usage
```

```
## <span style="color:#C39BD3 "> Adding framerate control and negotiation support to libcamera's GStreamer source element. </span>

With this functionality libcamerasrc can negotatie framerate of the stream.

Usage
```

```
## <span style="color:#98D435"> Contributions </span>

1.[Provide colorimetry <> ColorSpace mappings](https://git.libcamera.org/libcamera/libcamera.git/commit/?id=fc9783acc6083a59fae8bca1ce49635e59afa355)

2.[Provide mulitple colorimetry support](https://patchwork.libcamera.org/patch/17174/)

3.[Provide framerate support for libcamerasrc](https://patchwork.libcamera.org/patch/17307/)
