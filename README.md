# babbage

### a cheap, open-source, 3d-printable mobile manipulator.

![babbage](docs/images/babbage.jpg)

babbage is a small mobile robot with a holonomic drivetrain, a 4-dof arm, a webcam, and a raspberry pi.

the idea is pretty simple: **make a robot that you can actually build.**

it's still very much a work in progress, but the current prototype can drive around, detect apriltags, move toward them, and the user can teleoperate its arm well enough to poke an apriltag cube.

the gripper is currently the thing standing between "poke the cube" and "actually pick up the cube."

## what is it?

babbage is a platform for messing around with robotics without needing a robotics lab.

the base uses a 4-wheel holonomic x-drive with omniwheels, while a 4-dof arm sits on top. a raspberry pi handles the higher-level software and a webcam provides the robot's eyes.

the current hardware is intentionally pretty basic:

* raspberry pi 5 1gb (pi 4 or newer should work too)
* 4 × ga25-370 dc gearmotors
* 4 × omniwheels
* tb6612fng motor driver
* pca9685 servo controller
* a collection of hobby servos (current version uses 2 MG996Rs, a DS3218 30kg/cm servo, and an MG90 for the wrist joint.)
* usb webcam
* 12v power (current prototype im releasing is tethered, and relies on an external wall plug)
* a lot of 3d printed plastic

the ga25-370s actually have quadrature encoders, but babbage doesn't use them yet. the drivetrain is currently open-loop because it's part of the future goal for babbage-vla, a compute cheap VLA that can run on a PC like an m1 Mac Mini and have it control babbage.

## what can it do?

right now:

* drive around
* move in any direction with the holonomic drivetrain
* detect apriltags
* drive toward apriltags
* teleoperate the arm
* move the arm toward an apriltag cube
* run the whole thing from a raspberry pi (i use a pi 5 1gb)

eventually:

* actually pick things up
* autonomous manipulation
* proper localization
* encoder-based odometry
* better motion planning
* and, hopefully, considerably more intelligent things

## the bigger idea

the long-term goal isn't really just to make one robot.

i want babbage to be a cheap physical platform for experimenting with things like computer vision, robotics, imitation learning, reinforcement learning, and embodied ai.

ideally, you should be able to tell it something like:

> "go find the red cube and put it on the table."

and have a VLA figure out which robot functions it needs to call to make that happen.

and eventually, if i can afford to build more than one of these things, i'd love to experiment with multiple babbages working together.

that's a problem for future me.

## building one

the mechanical parts are designed in fusion and are intended to be printable on relatively normal consumer 3d printers.

so far i've tested everything in pla on an ender 3 v3 se. petg should work too, although i haven't done nearly as much testing with it.

the goal is to release both the editable source files and simpler stls so you don't need to know cad just to build the robot.

the repo will include:

* fusion source files
* stls
* wiring diagrams
* firmware
* python software
* assembly documentation
* parts lists

the exact bill of materials is still being figured out, but a complete build should land somewhere around **$250 cad-ish**, depending heavily on where you source everything and how aggressively you shop for parts.

## software

babbage runs python on the raspberry pi.

there isn't a giant software stack hiding underneath it. the idea is to keep things understandable enough that someone who is new to robotics can actually read the code and figure out what's happening.

the pi handles the higher-level stuff while the motor and servo controllers handle the actual hardware.

```text
                 ┌───────────────┐
                 │  raspberry pi │
                 │               │
                 │    python     │
                 └───────┬───────┘
                         │
              ┌──────────┴──────────┐
              │                     │
       ┌──────▼──────┐       ┌──────▼──────┐
       │  tb6612fng  │       │   pca9685   │
       │             │       │             │
       └──────┬──────┘       └──────┬──────┘
              │                     │
        4 × ga25-370          4-dof arm
```

## roadmap

this thing is going to change a lot.

### mechanical

* [x] holonomic drivetrain
* [x] 4-dof arm
* [ ] proper gripper
* [ ] improve arm design
* [ ] improve drivetrain
* [ ] finalize printable parts

### electronics

* [x] raspberry pi control
* [x] tb6612fng motor control
* [x] pca9685 servo control
* [x] 12v power system
* [ ] encoder support
* [ ] better power distribution
* [ ] maybe a custom pcb eventually

### software

* [x] basic driving
* [x] teleoperation
* [x] webcam support
* [x] apriltag detection
* [x] apriltag navigation
* [x] arm control
* [ ] autonomous grasping
* [ ] localization
* [ ] motion planning
* [ ] autonomous task execution

### ai

* [ ] llm-controlled robot functions
* [ ] autonomous task planning
* [ ] babbage-vla
* [ ] multi-babbage cooperation

## why "babbage"?

because charles babbage built machines that were wildly ahead of what was practical at the time.

also, "babbage" sounded better than LoCAR

## contributing

babbage is open source, and i'd like other people to mess with it.

if you build one, redesign something, make a better gripper, add a sensor, improve the software, or just do something stupid with it that i didn't think of, i'd love to see it.

the project is intentionally still a little rough, that's kind of the whole point.

---

**babbage is a robot you can build, modify, break, and teach things to.**

go crazy!
