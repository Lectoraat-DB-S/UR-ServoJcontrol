# UR-ServoJcontrol

The servoj command can be used for online realtime control of the joint positions in UR cobots. This can be used to move the cobot smoothly through (a large number) of waypoints. This can especially be helpfull for situations where:

- waypoints are not fixed (e.g. generated based on script or external input),
- future waypoints are not known in advance
- a large number of waypoints have to be followed and/or where using a blendradius is not practical
