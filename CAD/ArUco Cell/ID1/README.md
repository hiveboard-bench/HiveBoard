# ArUco cell — ID 1

This cell uses **OpenCV `DICT_4X4_50`, marker ID `1`**. It shares the mounting dimensions and printing method of the ID 0 cell. Use it when an additional marker is needed on the board.

| File | Use |
|---|---|
| [aruco_cell_id1_base_white.obj](aruco_cell_id1_base_white.obj) | Print in white PLA |
| [aruco_cell_id1_marker_black.obj](aruco_cell_id1_marker_black.obj) | Print in black PLA |
| [aruco_cell_id1_assembly.obj](aruco_cell_id1_assembly.obj) | Assembly reference |
| [aruco_cell_id1_assembly.mtl](aruco_cell_id1_assembly.mtl) | Shared OBJ display materials |
| [aruco_cell_id1_assembly.usdz](aruco_cell_id1_assembly.usdz) | Assembly with original USD materials |

Keep the shared MTL beside all three OBJ files. Each component was extracted from the supplied assembly without changing its geometry. The two parts are printed separately, fitted together, and optionally glued at the mating surfaces.

OBJ coordinates are in centimetres. Import at ×10 into millimetre-based software. The assembled dimensions are **88.1 × 76.297 × 22.0 mm**. The USDZ declares millimetre units and should be imported using that metadata. Its supplied material names and appearance are preserved. Use black PLA for the marker insert regardless of the displayed material.

The nominal outer black square is **47.505 mm** per side. Measure the printed square for pose estimation. Record the ID and marker-to-board transform separately from those of ID 0.

See the [ArUco cell guide](../README.md) for printing, assembly, camera calibration, and placement.
