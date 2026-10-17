# Ball valve — 360° variant

This variant allows the lever to rotate freely through 360°. It was designed for policy development, data collection, and controller debugging, where commands may overshoot the usual 90° ball-valve motion. Allowing continued rotation reduces the risk of breaking the mechanism by driving into a quarter-turn stop. It does not establish a load rating or guarantee against other forms of damage.

## Files

| File | Use |
|---|---|
| [ball_valve_360_base.obj](ball_valve_360_base.obj) | Separate base body |
| [ball_valve_360_lever.obj](ball_valve_360_lever.obj) | Separate lever body |
| [ball_valve_360_assembly.obj](ball_valve_360_assembly.obj) | Assembled reference |
| [ball_valve_360_assembly.mtl](ball_valve_360_assembly.mtl) | Shared OBJ display materials |
| [ball_valve_360_assembly.usdz](ball_valve_360_assembly.usdz) | Packaged assembly with original USD materials |

Keep the shared MTL file beside all three OBJs. The base and lever were separated from the supplied assembly by body, preserving the original coordinates and faces. Use the assembly to check fit and orientation. These releases contain mesh and USDZ exports. STEP, STL, and an articulated simulator configuration are not included for this variant.

## Scale, printing, and assembly

OBJ coordinates are in centimetres. Multiply them by 10 for a millimetre-based importer or by 0.01 for a metre-based simulator. The mounting base is **88.1 mm** wide. The assembly occupies approximately **162.3 × 76.3 × 66.1 mm** in the exported pose.

The USDZ declares millimetre units (`metersPerUnit = 0.001`). Respect that metadata when importing it.

Print the base and lever as separate parts using the [recommended PLA settings](../../../../README.md#recommended-3d-printing-settings). Remove support material and stringing, fit the parts as shown in the assembly, and check a full revolution by hand before using the robot. Keep the full swept path of the lever clear of neighbouring attachments and the fixture. Check friction-ring fit separately if adding a ring.

## Task and experiment records

The standard Ball valve task remains a **90° rotation from closed to open**. The 360° variant changes the mechanism's permitted travel, not the task target. Mark the initial and target orientations when using it for a quarter-turn experiment.

Record `ball_valve_360`, the asset commit, any friction ring, and the task target in the setup description or dataset metadata. In the website Evaluation Runner, use **Calibration notes** for the variant and setup details. Report this hardware variant explicitly when comparing results with the standard valve. Training episodes with a full-turn target must state that target separately.

The existing benchmark still has **13 conditions with five trials each**. This variant adds no new scored condition.

## Simulation

The USDZ contains geometry and materials, with no physics joints or rigid-body configuration. A simulator integration must define the rotation axis, joint type, collision shapes, masses, and friction, and validate the resulting motion against the physical mechanism. Existing HiveBoard simulator assets continue to describe their own released valve geometry.

See the [documentation guide](https://hiveboard-bench.github.io/hivedocs/hardware/ball-valve-360) for use and reporting.
