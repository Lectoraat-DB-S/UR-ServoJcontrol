# UR-ServoJcontrol

The servoj command can be used for online realtime control of the joint positions in UR cobots (see also UR scripting manual). This can be used to move the cobot smoothly through (a large number) of waypoints. This can especially be helpfull for situations where:

- waypoints are not fixed (e.g. generated based on script or external input),
- future waypoints are not known in advance
- a large number of waypoints have to be followed and/or where using a blendradius is not practical
- a custom trajectory from a trajectory function (e.g. follow a sine wave) has to be followed

For optimal performance, it is recommended to update the target position at maximum frequency (500 Hz), thus t=0.002. Note the specified target position is in joint coordinates (the angle of each of the cobot joints), which can be generated from TCP coordinates via the get_inverse_kin function.

The ServoJ_example.script provides an example for moving over a skew sinewave based trajectory for the TCP for a period of 5 seconds (resulting in a trajectory with 2500 target positions). Subsequently it provides a rectangular motion of the TCP.


## Remarks:
To obtain smooth motion of the cobot, the user has to provide a smooth input trajectory. This means that the motion profile and the derivative of the motion profile (velocity) has to be at least a continous functio . Ideally, the motion profile, velocity profile, and the acceleration profile (second derivative) are all a continous and smooth function to minimize vibrations.

An approach to ensure a smooth motion profile is to use a skew sine to generate the trajectory. A skew sine moves from 0 to 1 with halve of a sine-wave, which due to its properties, provides a smooth derivative and second derivative (and third derivative....). This skew sine function which goes from 0 to 1 can be implemented by using:

$$y = 0.5 - 0.5*cos(x) \qquad \text{for} \qquad 0 \leq x \leq \pi $$

In example, to move from value (or position) $A$ to $B$ with a skew sine in a time period of 3 seconds:

$$P(t) = A + (B-A)*(1/2-1/2*\cos(t/3*\pi)

with $P$ the target position at each time step $t$. In the example script, the elapsed time is tracked by the counter $i$, which combined with the timestep $dt$, provides the total elapsed time.
