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
./SensorViewer -cam ximea:[id0=33472151,id1=33470951,sync=2]// -imu microstrain://
```


