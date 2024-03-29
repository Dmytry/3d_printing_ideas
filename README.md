# Various ideas published to establish prior art, mostly 3D printing related. 

## Pythagoras:

https://youtube.com/playlist?list=PLt8GA9Tif0MCI780DuS0Yf162f6rO9wMg

## Marionette printer, complete:

https://youtu.be/riSgp-WCRXw

# Statics


## 3D printer kinematics

Consisting of a sliding bearing on a flat surface, moved around by an arrangement of cables. The print head is mounted upon the bearing. 

The bearing block's mass can be partially decoupled from high frequency components of the motion of the printhead through the use of a flexure pivot with damping.

The flat surface could have positioning information for closed loop positioning and/or calibration information. For example the surface could be glass, with the positioning information engraved on the back of the glass, read optically. Or a ferromagnetic surface could have magnetic positioning information.

## Cartesian version of the above

todo

## "Marionette" parallel cable robot cable tensioner (to avoid wasting motor torque on tensioning)

[Video](https://www.youtube.com/watch?v=OGiijvV2sIw)

[Motorized video](https://youtu.be/3ctT8vhLEVk)

A scaled down version of the cable robot (2D or 3D), with each cable replaced with a pivoting rod (performing identical movement), can be used to provide counter-tension on the ropes (the length of the rod sticking out behind the pivot is proportional to the cable length that needs to be drawn from the cable robot). Scaling can be done with block-and-tackle arrangement or coaxial winches or pulleys of different diameters, or any other scaling mechanism. Springs can be used to compensate for imprecision in the assembly.

![A pencil drawing of the above description](parallel_cable_robot_tensioner.png)

Only one cable is shown; all other cables work similarly, going to the corresponding rods.

## Compact version of parallel cable robot tensioner

A tapered conical winch takes up the amount of cable proportional to rotation angle squared.

That allows to mechanically compute square & square root.

A differential gearing or a block and tackle arrangement with 1 idler allows to compute a sum or difference. A constant can be added or subtracted by adding an offset.

Thus an arrangement of conical winches, cylindrical winches, and blocks and tackles or differentials can compute $l = \sqrt{x^2+y^2}$ for each cable in a parallel cable robot, from Cartesian xy or xyz position. 

## Rotary delta with cable drive, parallel SCARA with cable drive

jointly with Numbat from Armchair Engineering discord:

A rotary delta robot with cables used to drive "upper arms". The same mechanism as Pythagoras. 

Alternatively: 2 cables are used per arm, one as an extensor other as flexor, 
at least one cable goes to variable-diameter helical groove winch (through a spring to maintain tension) Other can go to a variable radius winch or a plain winch. Variable diameter winch is shaped to maintain cable tension as the motor rotates. 

![A pencil drawing of the above description](rotary_delta_cable_drive.png)

## Magnetic bed probe / simplified clicky / unclicky:

2 or 3 magnets attach the probe to the carriage when it is deployed, similar to Clicky and Unclicky probes (which were the direct inspiration). When the probe is pushed into the bed, one magnet disconnects. In the probe, magnets are connected with a wire, on the dock sense wires are attached to the magnets.

![A pencil drawing of the above description](rocking_bed_probe.png)

Possible variations: an omnidirectional probe (similar to CNC probes) for probing edges of the bed.

## Fully constrained tensegrity straight line mechanism (e.g. for bed or xy frame movement in a 3D printer or generally for linear movement without the use of linear rails):

[Video](https://youtu.be/cEeoZqRsgvY)

[Alternative cable arrangement](https://www.youtube.com/watch?v=tocf8PchpOw)

A print bed is supported on 6 cables that are arranged such that they are not kinematically redundant, and there is 6-DOF rigidity (like Stewart platform). A possible arrangement could have cables coming from the middles of 3 sides of a rectangle to the corners of another rectangle. Alternatively the cables may cross one another. Software can be used to find the best arrangement of cables for the purpose.

All cables are winched together at the same rate. The winches can use a helical groove to keep cable from overlapping itself. The winches could be constant or variable diameter (tapered).

If gravity or springs are inadequate for counter-tension, counter-tension can be provided by one or more cables placed in opposition to the 6 positioning cables, would onto a variable-diameter pulley on the same shaft (they wind in the opposite direction). The variable diameter pulley is shaped to ensure that correct length of cable is metered out.
Adding springs to extra cables eliminates backlash and allows for slight imprecision in the mechanism, avoiding issues with overconstraint.

## Other tensegrity straight line mechanisms

Easy to make a straight line mechanism with variable-diameter winches. Pretty much cheating.

# Dynamics

## Decreasing inertial forces for short duration accelerations, improving acceleration performance

If an object accelerates to a given speed over a given distance $L$, the acceleration can be computed as $a = {{v^2}\over{2L}}$ . Notably, required acceleration is lower if the distance is greater.

Typical high-acceleration 3D printing move commands consist of a short acceleration phase followed by coasting. 

For example the print head may accelerate to $0.5 m/s$, over the distance of $1 mm$, requiring the acceleration of $125 m/s^2$ (which is somewhat over the limit of current consumer grade 3D printing technology)

Only the position of print head orifice matters for printing quality, however. Slight rotations of the nozzle around the orifice are permissible.

A print head consists of a number of masses, not all of which have to accelerate over the same distance. Fans and other components (e.g. the extruder, also see Flying Extruder on Delta printers) can lag slightly behind the print head.

The "lagging masses" need to be damped with regards to printhead to avoid resonant built up.

## 3D printer hotend assembly on an universal joint flexure or other mechanism with a virtual pivot point at the nozzle orifice. 

Allows use of much of the hotend (or another tool) mass as part of a tuned mass damper, allows partial decoupling from short duration accelerations.

# Ping pong (impulse) based movement

Instead of continuously coupling motors to print head, the motors are coupled through an impact clutch (similar to an impact driver). The motors are disconnected from print head prior to an acceleration, a speed is set up on the motors such that engaging the clutch elastically bounces the print head in the desired direction (similarly to bouncing a ball off a moving ping-pong paddle, but in the printer's kinematic space). A continuously variable transmission may also be used to rapidly set up the velocity without having to accelerate or decelerate a motor rotor.

A possible simple version can use large-backlash couplings (e.g. 350 degrees worth of backlash) to allow the motor a "runway" to accelerate decoupled prior to impact.

A possible implementation: 3 motors per axis, 1 motor is directly coupled to the shaft, 2 more are connected through impact couplings (implemented as a purely passive large-backlash coupling, or actively controlled). 

Motor 1 drives the shaft at approximately constant speeds in the moves, without regards for its acceleration limit. The other two motors apply impacts in either direction by spinning up and having the coupling engage when the velocity needs to be abruptly changed.

# Scope

While those ideas were initially conceived in relation to the 3D printing, they are generally applicable to a broad range of robotics, including but not limited to: welding, machining, laser etching, pick-and-place, etc.

## Novelty

Who knows? All these ideas are probably 100+ years old in some other context, but people had been patenting use of 100+ year old inventions in the context of 3D printing so it's better to put things clearly in writing with a clear timestamp.

# Sensors

Filament mass sensor that measures filament mass in a given interval by measuring resonance frequency of a resonator that includes a length of the filament. Filament is held between two rollers and vibrated at the natural resonance frequency, additional set of driven "follower" rollers eliminate effects of filament outside the measurement zone. Alternatively the resonator has sufficiently stiff springs that stiffness of the filament is relatively insignificant in comparison.

Capacitive filament diameter sensor that measures filament all around by measuring change in the average dielectric constant within the measurement zone. Possible difficulties: water has very large dielectric constant. Although that can be made use of for moisture content measurements.

# Hotends

Making a 90 degree nozzle by bending a metal tube (instead of machining as in Positron hotends).

A 90 degree attachment for any hotend, consisting of a 90 degree bent tube with the nozzle on one end and flared out other end. The tube is retained inside the heatblock using a bolt with a hole in the middle matching the tube diameter. That would allow pointing the nozzle in arbitrary direction regardless of how the threads start.

A 360 or more degree bent tube in the hotend, with the idea that if the inside of the filament is colder than the outside, it would have different elastic properties and would end up pushed towards the outer wall (similarly to convection), improving heat transfer to the plastic. 

Deforming (squishing) a tube to increase contact surface area, instead of adding any conductive material inside the tube (may or may not be a viable work-around for EP3445568A1).

## Rigid support for the hotend

![An illustration of an octohedral strut hotend mount. 6 edges of an octahedron are used as a structure.](hotend_mount_ring.png)

The mount is used to rigidly couple the heatblock to the toolhead, heatsink, or the like.

The rods are made of thin low thermal conductivity material (e.g. stainless steel, titanium, thungsten, etc). The rods could be metal screws. 6 rods provide full 6-DOF rigidity without impacting bending force upon the rods, allowing very lightweight, low thermal conductivity construction.

# Existing patents

Who knows? I don't know one way or the other.
