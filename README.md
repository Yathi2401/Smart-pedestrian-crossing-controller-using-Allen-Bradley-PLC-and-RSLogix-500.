# Smart Pedestrian Crossing Controller using Allen-Bradley PLC

This project is a PLC-based smart pedestrian crossing controller developed using **RSLogix Micro Starter Lite**, **RSLogix Emulate 500**, and **RSLinx Classic**.

The system is designed for a straight-road pedestrian crossing where vehicles normally have priority. When a pedestrian presses the crossing button, the PLC stores the request and safely changes the traffic sequence before allowing the pedestrian to walk.

## Project Overview

The controller uses ladder logic to manage vehicle signals, pedestrian signals, request memory, timers, night mode, emergency mode, and fault handling.

The main operating sequence is:

1. Vehicle green is active during normal operation.
2. Pedestrian presses the request button.
3. PLC stores the pedestrian request.
4. System waits until the minimum green time is complete.
5. Vehicle signal changes from green to yellow.
6. Vehicle signal changes to red after yellow timing.
7. Red clearance delay is completed.
8. Pedestrian walk light and buzzer turn ON.
9. After the walk timer finishes, the system returns to vehicle green.

## Features

- Start and stop control using seal-in logic
- Vehicle green, yellow, and red signal control
- Pedestrian push button request
- Pedestrian request latch memory
- Pedestrian walk signal
- Pedestrian stop signal
- Pedestrian buzzer output
- Request lamp output
- Minimum green timer
- Yellow timer
- Red clearance timer
- Walk timer
- Night mode yellow flashing
- Emergency mode handling
- Fault detection and fault lamp indication
- Timer reset logic for repeated operation
- State-based control using internal PLC memory bits

## Software Used

- RSLogix Micro Starter Lite
- RSLogix Emulate 500
- RSLinx Classic

## PLC Logic Method

This project uses a **state-based ladder logic structure**. Each main stage of the crossing sequence is controlled using internal memory bits.

Main states:

| State | Description |
|---|---|
| Green State | Vehicles are allowed to move |
| Yellow State | Vehicles receive warning before red |
| Red Clearance State | Short safety delay before pedestrian walk |
| Walk State | Pedestrian walk light and buzzer are active |

Latch and unlatch instructions are used to move between states. Timers are used to control the duration of each stage.

## PLC Address Summary

| Address | Description |
|---|---|
| I:0/0 | Start push button |
| I:0/1 | Stop button |
| I:0/2 | Pedestrian push button |
| I:0/3 | Emergency switch |
| I:0/4 | Night mode switch |
| B3:0/0 | System run seal-in bit |
| B3:0/1 | Green state |
| B3:0/2 | Yellow state |
| B3:0/3 | Red clearance state |
| B3:0/4 | Walk state |
| B3:0/5 | Pedestrian request stored |
| B3:0/6 | Minimum green active |
| B3:0/7 | Emergency mode active |
| B3:1/0 | Fault bit |
| B3:1/1 | Flash bit |
| B3:1/2 | Night mode |
| O:0/0 | Vehicle green output |
| O:0/1 | Vehicle yellow output |
| O:0/2 | Vehicle red output |
| O:0/3 | Pedestrian walk output |
| O:0/4 | Pedestrian stop output |
| O:0/5 | Pedestrian buzzer output |
| O:0/6 | Request lamp output |
| O:0/7 | Fault lamp output |

## Timer Summary

| Timer | Purpose |
|---|---|
| T4:1 | Yellow timer |
| T4:2 | Red clearance timer |
| T4:3 | Walk timer |
| T4:4 | Minimum green timer |
| T4:5 | Flash ON timer |
| T4:6 | Flash OFF timer |

## Operating Modes

### Normal Mode

In normal mode, the vehicle green light remains ON until a pedestrian request is received. After a valid request and minimum green timing, the system changes to yellow, then red clearance, then pedestrian walk.

### Night Mode

Night mode disables the normal crossing sequence and makes the vehicle yellow light blink using a timer-generated flash bit.

### Emergency Mode

Emergency mode stops the normal sequence and resets active states. This prevents the controller from continuing a normal crossing cycle during an emergency condition.

### Fault Mode

Fault mode activates a fault indication and prevents the normal pedestrian crossing sequence from continuing during a fault condition.

## Documentation

The ladder logic screenshots are included in the project PDF:

```text
Smart_Pedestrian_Crossing_PLC_Documentation.pdf
```

## Project Files

```text
README.md
Smart_Pedestrian_Crossing_PLC_Documentation.pdf
Smart_Pedestrian_Crossing_PLC_Project.rss
```

## Learning Outcomes

Through this project, I practiced:

- PLC ladder logic programming
- Allen-Bradley addressing
- XIC and XIO instructions
- OTE, OTL, and OTU instructions
- TON timer instructions
- Counter instruction usage
- Timer reset logic
- Internal memory bit control
- State-based automation logic
- Traffic signal sequencing
- Fault and emergency handling
- PLC simulation using RSLogix Emulate 500

## Possible Program Improvements

Future improvements that can be added to the PLC program include:

- Extend the system from a single straight-road pedestrian crossing to a four-way junction traffic light controller.
- Add separate signal states for north-south and east-west vehicle directions.
- Add pedestrian crossing logic for all four sides of the junction.
- Add turn signal control for right-turn or left-turn lanes.
- Add vehicle sensor inputs to detect traffic waiting at each road.
- Add priority control for emergency vehicles.
- Add separate timing presets for peak hours, normal hours, and night mode.
- Add conflict prevention logic so opposite or unsafe signals cannot turn ON together.
- Add more detailed fault handling for each direction and each signal lamp.
- Add HMI monitoring to show active junction state, timers, requests, and faults.

## Project Status

The project ladder logic has been developed and tested using RSLogix Micro Starter Lite and RSLogix Emulate 500. The controller successfully performs the main pedestrian crossing sequence, including vehicle signal control, pedestrian request handling, walk signal operation, buzzer indication, night mode flashing, and fault/emergency handling.
