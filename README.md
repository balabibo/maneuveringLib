![OpenFOAM v2506](https://img.shields.io/badge/OpenFOAM-v2506-brightgreen.svg)

# maneuveringLib

##### An OpenFOAM library focused on free-running maneuvering simulations

## Summary

These libraries can be used with solver which deals with rigid-body motion, such as `overInterDyMFoam`, `waveDyMFoam` if you compile the `waves2Foam`. The main purpose of this serial is to realize the free-running maneuvering motions of ship in OpenFOAM, including self-propulsion, turning, zigzag and coursekeeping.

![gif in ./image](./image/out.gif  "Turning in calm water")

![gif in ./image](./image/output.gif "Turning in waves")


## Installation


### Compile from source files

```sh
git clone https://github.com/balabibo/maneuveringLib.git
cd maneuveringLib
./Allwmake
```

## Features
  1. Modified the storage structure of rigidBodyState dictionary. Now you can change the number of Degree of freedom (DoF) when you modify the dynamicMeshDict in `/constant` directory.
  2. add two solidBody motions `driven3DofMotion` `driven2DofMotion` in `/src/meshTools/solidBodyMotionFunctions`. It was modified from `drivenLinearMotion`, and it can realize the following rotation of background mesh region, which is useful for maneuvering motions like turning or zigzag.
  3. add two momentum source methods `oumSource` `HOSource` in `/src/fvOptions/sources/derived`. They are based on blade element momentum theory/open water curve seperately, and you can find details from the reference, it can be used to replace the real propeller as a propulsion device.
  4. add 4 different maneuvering motions, self-propulsion, turning, zigzag and coursekeeping, for ship. First, it utilize the PID controller to adjust the revolution speed of discretized propeller or momentum source in "sailing" mode, and the PID contorller is also applied to control the rudder motion in "coursekeeping" mode. The rudder controller is used to realize "turning" and "zigzag" maneuvering motions.

## Updates:
  1. rewrite class `maneuveringOutput`, class `maneuveringInput`, class `controlMethod` with RTS construction.
  2. the loaction for `driven3DofMotion` `driven2DofMotion` is updated.

#### P.S.

This serial will be updated continuously in the future. Those modules may have some bugs due to the neglect of author, and if you have any question or suggestion, please feel free to use the "Issues" button.
