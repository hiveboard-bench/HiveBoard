# HiveBoard

<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="Images/HIVEBOARD_logo_dark.png">
    <source media="(prefers-color-scheme: light)" srcset="Images/HIVEBOARD_logo_light.png">
    <img alt="HiveBoard logo" src="Images/HIVEBOARD_logo_light.png" width="50%">
  </picture>
</p>

[Project website](https://hiveboard-bench.github.io) · [Documentation](https://hiveboard-bench.github.io/hivedocs/) · [Evaluation Runner](https://hiveboard-bench.github.io/hivedocs/benchmark/evaluation-runner) · [Demonstration video](https://youtu.be/kaYB_Oc64nA)

HiveBoard is a modular, 3D-printable benchmark of industrial mechanisms for robotic and prosthetic manipulation. Its attachments require constrained motions such as valve rotation, threading, key insertion, and drawer opening and closing.

A seven-cell honeycomb base accepts interchangeable attachments through a shared press-fit interface. The same board and protocol can be used to evaluate robot grippers, dexterous hands, teleoperated manipulators, and worn prosthetic hands.

This repository contains the printable parts, CAD models, articulated simulation assets, evaluation protocol, and trial templates.

## Getting started

1. Read the [printing guide](https://hiveboard-bench.github.io/hivedocs/hardware/printing) and the recommended settings below.
2. Print one honeycomb cell and one attachment base to check the press fit before printing the full set.
3. [Assemble and mount the board](https://hiveboard-bench.github.io/hivedocs/hardware/assembly). Check that each mechanism moves freely and each attachment remains seated.
4. Read the [evaluation protocol](Documentation/PROTOCOL.md), including familiarization, success criteria, timeouts, and counting conventions.
5. Record **five trials for each of the 13 conditions (65 trials total)** using the [Evaluation Runner](https://hiveboard-bench.github.io/hivedocs/benchmark/evaluation-runner) or the [CSV](Documentation/trials.csv) / [XLSX](Documentation/trials.xlsx) template.

The documentation and Evaluation Runner are maintained in [`docs/` in the project website repository](https://github.com/hiveboard-bench/hiveboard-bench.github.io/tree/main/docs).

## Board and attachments

<p align="center">
  <img src="Images/Hiveboard4.png" alt="HiveBoard honeycomb base with mounted mechanisms" width="50%">
</p>

HiveBoard has 12 attachment designs evaluated in 13 conditions. The ball valve is evaluated without and with a friction ring, giving two conditions for the same attachment design. Attachments share the same mounting geometry. The shock absorber occupies two adjacent cells. The ball valve is evaluated in two configurations: without a friction ring and with a ring fitted.

<p align="center">
  <img src="Images/attachments_overview.png" alt="HiveBoard mechanisms shown on the base and as individual renders" width="100%">
</p>

| Category | Attachment | Task |
|---|---|---|
| Torque | Ball valve | Rotate the lever 90° from closed to open |
| Torque | Ball valve + ring | Complete the same rotation with the ring fitted |
| Torque | Gate valve (small) | Rotate the stem one full turn |
| Torque | Gate valve (large) | Rotate the stem one full turn |
| Torque | Circuit breaker | Move the toggle to the opposite state and hold it |
| Precision | Light bulb | Thread the bulb until seated |
| Precision | Thread (M8) | Thread the bolt along the available length |
| Precision | Thread (M30) | Thread the bolt along the available length |
| Precision | Peg insertion | Align and thread the free 8 mm peg into the socket until seated |
| Composed assembly | Button | Open the cover and press the button |
| Composed assembly | Lock and key | Grasp the key, insert it vertically, and turn it to unlock |
| Composed assembly | Drawer | Grasp the handle, pull the drawer open, and push it closed |
| Composed assembly | Shock absorber | Grasp the loose part, align its hole with the pin, and insert the part fully onto the pin |

The friction-ring accessory includes four rings with different rotational resistance. Record the configuration used. The gate-valve criterion is **one full turn of the stem**; full travel depends on the printed thread pitch. For composed assembly tasks, record the last completed stage as well as the overall outcome.

See [the protocol](Documentation/PROTOCOL.md) for timeouts and stage definitions, and [Terminology](Documentation/TERMINOLOGY.md) for task names and trial identifiers.

## ArUco cell

The optional [ArUco cell](CAD/ArUco%20Cell/) provides a visual reference for board localization and alignment between physical and simulated scenes. Print the base in white PLA and the marker insert in black PLA, fit the parts together, and optionally glue the mating surfaces. The folder includes the two printable parts, an assembled model, a CAD reference image, and printing and assembly instructions.

## Recommended 3D printing settings

Use PLA and a consumer-grade FDM printer. A **300 × 300 mm build area** accommodates the complete honeycomb base without splitting it. Thread test pieces are included in [`STL/Threads/`](STL/Threads/) for checking print tolerances before producing the complete mechanisms.

Detailed assembly and printing instructions are available in the [attachment-specific printing guide (PDF)](https://github.com/user-attachments/files/29721347/HiveBoard.-.Module-Specific.Instructions.1.pdf).

### PLA profile

| Setting | Value |
|---|---|
| Material | PLA |
| Nozzle diameter | 0.4 mm |
| Layer height | 0.20 mm |
| Wall count | 4 |
| Top / bottom layers | 5 / 5 |
| Infill | 15–30%, according to part type |
| Print speed | 50 mm/s |
| Nozzle temperature | 200–220 °C |
| Bed temperature | 50–60 °C |
| Cooling fan | 100% |
| Supports | Only where required |
| Bed adhesion | Skirt or brim |

### Infill

| Part type | Infill |
|---|---|
| Base structure | 20% |
| Mechanical parts | 25% |
| Torque components | 30% |
| Threads | 25% |
| Decorative covers | 15% |

### Orientation

| Component | Orientation |
|---|---|
| Threads and screws | Vertical |
| Nuts | Flat |
| Valves | Handle up |
| Drawer | Largest face on the bed |
| Pegs | Vertical |
| Shock absorber parts | Sideways |

Remove stringing and support material, check mating surfaces, and test the threads by hand. Record sanding, lubrication, and dimensional adjustments with the evaluation. Inspect attachment seating before each session and after any displacement or damage.

## Evaluation and trial records

A complete evaluation contains **65 recorded trials**, including separate five-trial blocks for the two ball-valve configurations. Keep the platform configuration and control interface consistent within the recorded trial blocks.

For each trial, record:

- outcome: `success`, `fail`, `timeout`, or `safety_stop`;
- completion time in decimal seconds, for successful trials only;
- attempts counted from 1 and regrasps counted from 0;
- prehensile or non-prehensile strategy;
- last completed stage for composed assembly tasks; and
- one dominant failure cause for unsuccessful trials.

Use [`HOW_TO_FILL_TRIALS.md`](Documentation/HOW_TO_FILL_TRIALS.md) for the column definitions and allowed failure causes. Preserve trials involving broken or displaced parts and describe the event in `notes`.

### Browser-based evaluation

The [Evaluation Runner](https://hiveboard-bench.github.io/hivedocs/benchmark/evaluation-runner) displays task instructions and example videos, provides a countdown and timer, and exports the trial records. Begin the first commanded task motion when the countdown reaches zero. The evaluator determines whether the success criterion has been met.

Record every trial with an external camera, keeping the board, end-effector, and final task state visible. Once all 65 trial entries and required setup details are complete, the runner generates a results ZIP with the CSV, platform description, manifest, session backup, and recording filenames.

Attach the setup photograph in the runner or add it to the extracted ZIP as `setup.jpg`. Add the 65 recordings to `videos/` using the generated filenames. The runner saves records locally and does not upload submissions to the organizers.

## Simulation assets

[`Simulation/`](Simulation/) contains URDF and USD assets, visual and collision meshes, joint definitions, and nominal physical properties. The mechanisms use revolute, continuous, and prismatic joints. Threaded motion is represented by coupled rotation and translation; drawer, lock, and shock-absorber articulation is provided in the USD assets.

Friction, mass, and inertia are nominal values. Check joint motion, collision geometry, and physical parameters in the simulator used for an experiment, and report any parameter overrides.

Isaac Lab environments and training code are maintained separately in [hiveboard-bench/isaaclab-hiveboard](https://github.com/hiveboard-bench/isaaclab-hiveboard). See the [simulation documentation](https://hiveboard-bench.github.io/hivedocs/simulation/assets) for asset usage and the [Isaac Lab guide](https://hiveboard-bench.github.io/hivedocs/simulation/isaac-lab) for installation and commands.

## Reported evaluations

HiveBoard has been evaluated at four laboratories using:

| Platform | Control |
|---|---|
| Boston Dynamics Spot with Spot Arm | Native tablet teleoperation |
| LeRobot SO-101 | Leader–follower teleoperation |
| ANYbotics ANYmal with DynaArm | Virtual-reality controllers |
| Macao prosthetic hand | Worn on the operator's forearm |

Each platform ran all 65 trials. Results and demonstration videos are available on the [project website](https://hiveboard-bench.github.io). The original trial logs are held by the contributing laboratories and are not distributed in this repository.

## Repository contents

| Directory | Contents |
|---|---|
| [`STL/`](STL/) | Printable parts and thread test pieces |
| [`CAD/`](CAD/) | Source geometry and mesh exports |
| [`Simulation/`](Simulation/) | Articulated assets and meshes |
| [`Documentation/`](Documentation/) | Protocol, logging instructions, and CSV/XLSX templates |
| [`Images/`](Images/) | Photographs, logos, and renders |

For a new attachment, reuse the mounting interface and document its initial state, success criterion, timeout, and reset procedure. See [Adding an attachment](https://hiveboard-bench.github.io/hivedocs/guides/new-attachment).

## Citation

If you use HiveBoard in your research, cite the project paper:

```bibtex
@article{hiveboard2026,
  title   = {HiveBoard: An Open, Modular, 3D-Printed Benchmark of Industrial Mechanisms
             for Robotic and Prosthetic Manipulation},
  author  = {Godoy, Ricardo V. and de Souza, Enzo F. and de Lange, Rudy De-Xin and
             Negri, Juliano and Marsicano, Jo\~{a}o A. and van Halst, Victor and
             Elanjimattathil Vijayan, Aravind and Capezzuto, Gianluca and
             Angarola, Matheus P. and Tommaselli, Felipe A. G. and Milazzo, Giuseppe and Baptista, Rafael R. and
              van Berge, Meiko Adriana and Bezerra, Ranulfo and Lahr, Gustavo J. G. and Ferrari Gerez, Lucas and
              Bicchi, Antonio and Becker, Marcelo},
  journal = {Under review},
  year    = {2026},
  url     = {https://github.com/hiveboard-bench/HiveBoard}
}
```

## License

This project is intended for research, educational, and prototyping purposes.

