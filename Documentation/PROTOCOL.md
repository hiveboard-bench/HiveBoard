# HiveBoard: Data Collection Protocol

Use [Terminology](TERMINOLOGY.md) to match task names to trial identifiers and existing file names.

This document specifies the data each collaborating laboratory collects to validate HiveBoard, the modular dexterity board. The activity is operator-driven trials, robot-side performance characterization across attachments. Operators may control the manipulation system through a teleoperated arm or through a wearable interface or exoskeleton that drives a gripper or hand directly.

The objective is to demonstrate that the board is functional, reproducible, and discriminative across attachments and platforms. The protocol does not rank platforms against each other and does not characterize control interfaces or operators.

**Project resources:**
- Repository (STL, CAD, simulation assets, this protocol, trial logging template): https://github.com/hiveboard-bench/HiveBoard
- Project page: https://hiveboard-bench.github.io
- Demonstration video (board walk-through and example trials): https://youtu.be/kaYB_Oc64nA

---

## 1. Materials

- One printed HiveBoard base.
- One full set of attachments across all three categories (torque, precision, composed assembly), including the four-piece friction ring accessory set for the ball valve.
- A manipulation system, consisting of an end-effector (gripper or hand) plus a control interface. The control interface may be:
  - a teleoperated robotic arm with a standard interface (e.g., SpaceMouse, leader arm, VR controller), or
  - a wearable interface or exoskeleton driving the end-effector directly.

## 2. Printing Specifications

The canonical print profile lives in the project README. Summary, for convenience:

- **Material:** PLA, 1.75 mm filament.
- **Nozzle:** 0.4 mm.
- **Layer height:** 0.20 mm.
- **Walls:** 4 perimeters.
- **Top / bottom layers:** 5 / 5.
- **Print speed:** 50 mm/s.
- **Nozzle temperature:** 200 to 220 °C.
- **Bed temperature:** 50 to 60 °C.
- **Cooling:** 100%.
- **Adhesion:** skirt or brim.
- **Supports:** only where required.

**Infill, per part type:**

| Part type | Infill |
|---|---|
| Base structure | 20% |
| Mechanical parts | 25% |
| Torque components | 30% |
| Threads | 25% |
| Decorative covers | 15% |

**Print orientation:**

| Component | Orientation |
|---|---|
| Threads / screws | vertical |
| Nuts | flat |
| Valves | handle up |
| Drawer | flat on the largest face |
| Pegs | vertical |
| Shock absorber parts | sideways |

**Post-processing.** Remove stringing and check that mating surfaces seat fully before testing. Minor sanding of threaded surfaces may improve performance when printer calibration produces tight tolerances. If sanding is applied to any attachment, record it in the trial `notes` column.

## 3. Physical Setup

1. Fix the HiveBoard base to a rigid surface within the operator's working volume. The base may be mounted horizontally on a tabletop or vertically on a fixture. State which one in `platform.md`, since a vertical mount changes the approach direction for every attachment and makes press-fit release more likely.
2. Insert the attachments into their designated cells. Each attachment seats by press-fit; verify all attachments are fully seated before starting trials.
3. Position the manipulation system so that all attachments are reachable without base repositioning during a trial.
4. Photograph the setup and store the image as `setup.jpg`.

## 4. Trial Procedure

HiveBoard has 12 attachment designs evaluated in 13 conditions. The ball valve is evaluated without and with a friction ring, giving two conditions for the same attachment design.

For each `(platform, condition)` pair:

1. **Familiarization.** Run unrecorded practice trials until completion times stabilize. Record only after three consecutive practice trials complete within 20% of each other or within the timeout, whichever comes first.
2. **Recorded trials.** Run **5 recorded trials** per condition. The end-effector starts each trial from the same neutral pose for a given platform.
3. **Trial start.** Begin timing when the operator initiates the first commanded motion toward the attachment.
4. **Trial end.** Stop timing when the success criterion is met, when a safety event occurs, or when the timeout is reached.
5. **Reset.** Return the attachment to its starting state between trials. Re-seat the attachment in its cell if displaced.

The ball valve is run as two separate sets of 5 trials: once without the friction ring (`valve_ball`) and once with the ring fitted (`valve_ball_ring`).

No scripted assistance, replanning, or per-trial parameter tuning is permitted during recorded trials. A restarted approach within a trial counts as another attempt. Count a regrasp only when the end-effector releases the part and grasps it again. The initial grasp is not a regrasp. Attempts and regrasps are separate counts; neither starts a new trial.

6. **Broken or displaced parts.** If a printed part breaks or leaves its cell during a trial, record the trial as it stood, describe the damage in the `notes` column, and reprint or reseat the part before continuing. Do not silently rerun the trial. Printed mechanisms have failed under jittering or high-gain command signals in previous sessions, and those events are part of the result.

## 5. Per-Attachment Success Criteria and Timeouts

**Torque category**

| Attachment | Success criterion | Timeout |
|---|---|---|
| Ball valve | Handle rotated 90° from closed to open | 60 s |
| Ball valve + ring | Handle rotated 90° from closed to open with the ring fitted | 90 s |
| Gate valve (small) | Stem rotated one full turn from the closed position | 90 s |
| Gate valve (large) | Stem rotated one full turn from the closed position | 120 s |
| Circuit breaker | Toggle moved from one state to the other and held | 60 s |

**Precision category**

| Attachment | Success criterion | Timeout |
|---|---|---|
| Light bulb | Bulb fully threaded until seated | 120 s |
| Thread (M8) | Bolt fully threaded along available length | 120 s |
| Thread (M30) | Bolt fully threaded along available length | 120 s |
| Peg insertion | Free peg threaded into the empty socket until it seats | 120 s |

The gate valve criterion is one full turn of the stem, not travel from fully closed to fully open. A platform that can turn the stem once can repeat the motion, and the number of turns to full travel depends on the printed thread pitch, so full travel is not comparable across prints. If your trials ran to full travel, report the time to the first complete turn and note it in the `notes` column.

**Composed assembly category (stage-wise scoring)**

These attachments are scored at sub-task granularity. Record the last completed stage within the timeout.

| Attachment | Stages | Timeout |
|---|---|---|
| Button | (1) Open the cover (2) Press the button until actuation | 60 s |
| Lock and key | (1) Grasp key (2) Insert key vertically (3) Rotate to unlock | 180 s |
| Drawer | (1) Grasp handle (2) Pull open (3) Push closed | 120 s |
| Shock absorber | (1) Grasp the loose part (2) Align its hole with the pin (3) Insert the part fully onto the pin | 180 s |

A trial is a full success only if all stages complete within the timeout. Partial completions are recorded by their last completed stage in the `stage_reached` column.

## 6. Data to Log per Trial

Each trial fills one row of `trials.csv` (template provided alongside this protocol). See `HOW_TO_FILL_TRIALS.md` for column-by-column instructions.

### Logging conventions

These conventions exist because logs returned from different laboratories have disagreed on all five points, which leaves the columns incomparable until they are reconciled by hand.

| Column | Convention |
|---|---|
| `completion_time_s` | Decimal seconds, as a plain number. Not milliseconds, not a text string, not a clock time, not a date. Write `12.9`, not `12923`, not `12.9 s`, not `timeout`. Leave the cell empty when the outcome is not `success`. |
| `n_attempts` | Discrete attempts at the task within the trial, counted from 1. An attempt ends when the operator abandons the current approach and starts over. Corrective motions inside one continuous approach are not separate attempts. |
| `n_regrasps` | Times the end-effector released the part and closed on it again, counted from 0. A trial with one grasp and no release is 0. A platform that cannot regrasp records 0. |
| `stage_reached` | The number of the last stage the trial completed, from 0 to 3. A successful trial reaches its final stage. A trial that never completed stage 1 is 0. Fill only for the composed assembly attachments. |
| `strategy` | `prehensile` when the end-effector closed around the part and held it, `non_prehensile` when the part was driven by pushing or pressing, or by a finger or jaw entered into an opening without an enclosing grip. |

Fill `n_attempts`, `n_regrasps`, and `strategy` on unsuccessful trials as well. A failed trial still had attempts, and how a platform approached a part it could not complete is as informative as how it approached one it could.

For every trial whose outcome is `fail`, `timeout`, or `safety_stop`, record the dominant failure cause in the `failure_cause` column using this closed vocabulary:

| Cause | Meaning |
|---|---|
| `grasp_geometry` | The end-effector cannot engage the part in a stable grasp (shape, size, or access mismatch). |
| `kinematic_limit` | The platform cannot produce the motion the task requires (e.g., clean rotation about an axis). |
| `perception` | The operator could not see or judge alignment well enough to complete the task. |
| `slip` | A grasp was acquired but lost during execution. |
| `force_limit` | The grasp or actuation force the platform can produce is insufficient for the task, even though the grasp and the motion are otherwise correct (e.g., holding a screw against thread friction). |
| `control_precision` | The available control resolution was too coarse for the clearance or force the task requires. |
| `other` | None of the above; describe in `notes`. Use this for a trial ended by a broken printed part. |

Pick the single dominant cause per trial. Leave the column blank on `success` rows. The closed vocabulary is what makes failure modes comparable across laboratories, so use `other` plus a note only when nothing else fits.

Alongside `trials.csv`, each lab provides:

- `setup.jpg`, photograph of the physical setup.
- `platform.md`, short description of the manipulation system: end-effector (gripper or hand), control interface (teleoperated arm or wearable), board mounting orientation, and any relevant control mode or calibration notes.

## 7. Submission

Each collaborating lab returns a single archive containing:

- `trials.csv`
- `setup.jpg`
- `platform.md`

### Reproducibility checklist

- [ ] All attachments printed with the specified PLA profile and per-part-type infill.
- [ ] Each attachment seats fully in the base before trials begin.
- [ ] Familiarization completed for every attachment before recording.
- [ ] 5 recorded trials per condition, all logged in `trials.csv`. The ball valve appears twice, once without the friction ring and once with it.
- [ ] Timeouts enforced as specified.
- [ ] `failure_cause` filled from the closed vocabulary for every `fail`, `timeout`, and `safety_stop` row.
- [ ] `completion_time_s` in decimal seconds on every `success` row, and empty everywhere else.
- [ ] `n_attempts` counted from 1 and `n_regrasps` from 0, on failed rows as well as successful ones.
- [ ] `strategy` filled on every row.
- [ ] Any broken or reseated part described in `notes`.
- [ ] `setup.jpg` and `platform.md` included, with the board mounting orientation stated.
- [ ] No operator names or identifiers in any field.
