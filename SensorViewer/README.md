SensorViewer usage
==================

Usage
-----

`./SensorViewer [-p] [-cam URI] [-imu URI] [-posys URI] [-encoder URI] [-lidar URI]`

Most arguments are self-explanatory. With `-p` SensorViewer starts paused.

URIs
----

The URIs used by SensorViewer take the form `driver:[opt1=1,opt2=2]//path`.
Some commonly used examples,

```
./SensorViewer -cam log://~/path/to/file.log
./SensorViewer -cam ximea:[id0=33472151,id1=33470951,sync=2]// -imu microstrain:// -posys vicon://192.168.20.100[NinjaCar]
```

DRIVERS
----

These drivers are a part of HAL, but are described here since they can be used with sensor viewer

Split Driver
- Purpose: Crop an image, by defining the Regions of Interest (ROI's) in the image that you wish to keep.
- Usage
```
./SensorViewer -cam split:[roi1=0+0+640x480]//log://logfile.log
```
This will only select a region of size 640x480, starting at pixels (0,0) (top left corner of the image). You may specify several ROI's if you wish to select only specific regions of an image.

