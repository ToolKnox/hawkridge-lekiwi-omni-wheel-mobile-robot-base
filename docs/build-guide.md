# Build guide — LeKiwi Omni-Wheel Mobile Robot Base

Skill level: comfortable with a 3D printer, small screws, a Raspberry Pi and the Linux command line.
Time: about 34 hours of printing and 2 hours of assembly.

This guide covers the 5 V power-bank version of the base. For the full mobile manipulator you also need a built
SO-101 follower arm, and a leader arm for teleoperation (SO-ARM100 project: https://github.com/TheRobotStudio/SO-ARM100).

## 1. Print the parts

| File | Qty | Supports | Notes |
|---|---|---|---|
| `base_plate_layer1.stl` | 1 | if the slicer asks | bottom plate |
| `base_plate_layer2.stl` | 1 | if the slicer asks | top plate |
| `drive_motor_mount_v2.stl` | 3 | if the slicer asks | one per wheel |
| `servo_controller_mount.stl` | 1 | if the slicer asks | holds the bus servo adapter |
| `5v_power_bank_holder.stl` | 1 | if the slicer asks | keeps the power bank at the back of the bottom plate |
| `webcam_mount.stl` | 1 | if the slicer asks | base camera |
| `webcam_mount_wrist.stl` | 1 | if the slicer asks | wrist camera |
| `so100_gripper_cam_mount_insert.stl` | 1 | if the slicer asks | static gripper with an M3 nut pocket for the wrist mount |
| `modified_base_arm.stl` | 1 | tree supports | optional SO-101 base that bolts to the top plate |

PLA on any FDM printer. Tested settings: 0.2 mm layers, 15% infill. Auto-orient each part in the slicer.
STEP files for both webcam mounts are included so you can adapt them to another camera.

Wheel hubs are not included. You need a hub that joins the STS3215 servo horn to your omni wheel's bolt pattern.

## 2. Set the servo IDs

Do this before the servos go into the base. Connect one STS3215 at a time to the bus servo adapter and give the
three wheel servos IDs 7, 8 and 9 with the LeRobot motor setup script. The LeRobot LeKiwi guide shows the exact
command: https://huggingface.co/docs/lerobot/lekiwi

## 3. Wheel modules (make three)

1. Fix a servo in a drive motor mount with 4 M2 x 5 mm tapping screws.
2. Screw the mount to the bottom plate with 4 M3 x 12 mm screws.
3. Join the omni wheel, your hub and the servo horn, then fix the horn to the servo with its center screw.

## 4. Bottom plate and power

1. Press M3 nuts into the servo controller mount and the power bank holder. Screw both to the bottom plate
   with M3 x 12 mm screws.
2. Fit the bus servo adapter in its mount and chain the three wheel servos to it.
3. Put the power bank in its holder at the back of the bottom plate.
4. Wire the 5 V version like this:
   - Power bank USB-C to the Raspberry Pi 5 USB-C power input (USB-C to USB-C cable).
   - Power bank to the servo adapter DC jack (USB-C to 5.5 x 2.1 mm DC cable, 5 V).
   - Raspberry Pi USB-A port to the servo adapter USB-C port (USB-A to USB-C cable). This is the data link.

## 5. Top plate

1. Put the Raspberry Pi 5 in its case. The bought case has no screw tabs, so fix it to the top plate with strong
   double-sided tape or a hook-and-loop strap.
2. Mount the SO-101 follower arm with 4 M3 x 20 mm screws. The plate has holes for both the modified base and
   the original SO-101 base.
3. Feed the servo adapter USB cable, the Pi power cable and the arm servo wires up through the hole in the top plate.
4. Fix the top plate on the motor mounts with 4 M3 x 12 mm screws.

## 6. Cameras

The mounts were drawn for a small clip-on 1080p webcam. Check your camera against the mount before printing.

1. Fit the printed gripper insert to the SO-101 static gripper and press an M3 nut into its pocket.
2. Lock the wrist mount to the gripper with an M3 x 12 mm bolt. Put the camera in the mount and clamp it with
   2 M3 x 35 mm bolts and nuts in the rear holes.
3. Mount the base camera the same way at the front of the robot.
4. Plug both cameras into the Raspberry Pi USB ports.

## 7. Software

1. Flash Raspberry Pi OS (64-bit) to the microSD card and set up Wi-Fi and SSH.
2. Install Hugging Face LeRobot on the Pi and on your laptop.
3. Follow the LeRobot LeKiwi guide (https://huggingface.co/docs/lerobot/lekiwi): calibrate the base and the arm,
   start the robot host on the Pi, then drive from the laptop with the keyboard and the SO-101 leader arm.

## Screws used

| Screw | Qty | Where | Notes |
|---|---|---|---|
| M2 x 5 mm tapping | 12 | servos in motor mounts | |
| M3 x 12 mm | about 22 | mounts, plates, wrist camera | plus M3 nuts for the mounts |
| M3 x 20 mm | 4 | SO-101 arm to top plate | |
| M3 x 35 mm | 4 | camera clamps | often missing from assortments |

## Troubleshooting

- A wheel servo is not found: check its ID (7, 8 or 9), the bus cable and the DC power to the servo adapter.
- Cameras drop out or the Pi warns about low power: the Pi 5 limits USB current when its supply does not offer
  5 V at 5 A. Use a power bank with a strong 5 V output and keep the cables short.
- The base drifts in a circle: one servo is reversed or has the wrong ID; recheck the IDs and the calibration.

## Safety

Keep the robot on the floor, or on a large table with an edge guard, while you tune it. Disconnect the power bank
before you rewire the servos.
