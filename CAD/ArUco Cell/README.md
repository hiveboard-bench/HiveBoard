# ArUco cell

The ArUco cell provides a visual reference for locating HiveBoard in camera images. It can support board-pose estimation and alignment of physical and simulated scenes once the marker dimensions and its placement on the board are known.

The cell has two interlocking parts, printed separately in white and black PLA. The white base forms the hexagonal support and the white regions of the marker. The black insert completes the marker pattern. The parts fit together and can be glued after checking their alignment.

This is an optional accessory. The benchmark evaluation remains 13 conditions with five trials per condition.

## Marker IDs

Two cells are available: **ID 0** and **ID 1**, both using OpenCV `DICT_4X4_50`. Use different IDs when mounting both cells in the same scene, and record a separate marker-to-board transform for each cell. Both use the same mounting geometry and nominal marker size.

## Files

### ID 0

| File | Purpose | Material |
|---|---|---|
| [aruco_cell_base_white.obj](aruco_cell_base_white.obj) | Hexagonal base and white marker regions | White PLA |
| [aruco_cell_marker_black.obj](aruco_cell_marker_black.obj) | Black marker insert | Black PLA |
| [aruco_cell_assembly.obj](aruco_cell_assembly.obj) | Assembled reference with both parts in position | White and black |

### ID 1

The [ID1/](ID1/) directory contains:

| File | Purpose | Material |
|---|---|---|
| [aruco_cell_id1_base_white.obj](ID1/aruco_cell_id1_base_white.obj) | Hexagonal base and white marker regions | White PLA |
| [aruco_cell_id1_marker_black.obj](ID1/aruco_cell_id1_marker_black.obj) | Black marker insert | Black PLA |
| [aruco_cell_id1_assembly.obj](ID1/aruco_cell_id1_assembly.obj) | Assembled reference | — |
| [aruco_cell_id1_assembly.mtl](ID1/aruco_cell_id1_assembly.mtl) | Display materials shared by the three OBJ files | — |
| [aruco_cell_id1_assembly.usdz](ID1/aruco_cell_id1_assembly.usdz) | Packaged assembly with the original USD materials | — |

The ID 1 component OBJs were separated from the supplied assembly by body, preserving all vertex coordinates and faces. The OBJ materials display the intended white and black print colors. The USDZ retains its supplied materials. Select black PLA for the marker insert even if an importer displays it as gray.

Keep each OBJ beside its referenced MTL file. The MTL files assign the display colors. Choose the corresponding filament when slicing each physical part. The assembly OBJ shows the intended fit and orientation.

These are mesh exports. Vertex positions, faces, and exported scale are preserved from the supplied files. Filenames, object groups, and material names have been standardized in English, and the OBJ material links have been updated.

## Printing and assembly

1. Import the white base and black insert into the slicer as separate parts. Set the import units to centimetres, or apply a scale factor of 10 if the slicer interprets OBJ coordinates as millimetres. Apply the same scale to both parts and verify an assembled width of 88.1 mm.
2. Print the base in white PLA and the insert in black PLA. Use the repository's recommended PLA profile as a starting point and inspect the mating surfaces for stringing or excess material.
3. Fit the two parts together in the orientation shown in the assembly model. Check that the marker pattern is complete and the insert is fully seated.
4. If permanent assembly is required, apply a small amount of PLA-compatible adhesive to the mating surfaces. Keep adhesive away from the visible marker face. Let it cure before mounting.
5. Seat the assembled cell in the honeycomb base and check that it remains fixed. Keep the marker visible to the camera during use.

## Dimensions and marker configuration

Both IDs have an overall width of **88.1 mm**. The OBJ coordinates therefore correspond to centimetres. The files retain their original coordinates. The ID 1 USDZ declares millimetre units (`metersPerUnit = 0.001`) and has the same physical dimensions. Use its declared units when importing it.

| Dimension | Nominal size |
|---|---|
| Assembly bounding box | 88.1 × 76.297 × 22.0 mm |
| Outer black marker square | 47.505 mm per side |

For a millimetre-based importer, multiply the OBJ coordinates by 10. For a metre-based simulator, multiply them by 0.01. Check the imported dimensions before printing or using the model in simulation.

The marker was generated with [chev.me/arucogen](https://chev.me/arucogen/) using **4×4 (50, 100, 250, 1000)**, with **marker IDs 0 and 1**. Configure the detector with **OpenCV `DICT_4X4_50`** and the ID of the printed cell. These IDs have the same bit patterns in `DICT_4X4_50`, `DICT_4X4_100`, `DICT_4X4_250`, and `DICT_4X4_1000`, which share the same underlying marker list in [OpenCV](https://github.com/opencv/opencv/blob/4.x/modules/objdetect/src/aruco/aruco_dictionary.cpp). Verify detection on the printed part. For pose estimation, measure the square marker side from the outer edges of its black border and use calibrated camera parameters. Record the marker's location and orientation relative to the board so that its estimated pose can be converted to a board pose.

Record the dictionary, marker ID, measured marker side length, model scale, and marker-to-board transform for each installed cell. Use unique IDs within the camera's view so each detection can be associated with its own transform. Detection accuracy and physical-to-simulation alignment need to be measured in the intended camera and lighting configuration.

See the [OpenCV ArUco detection documentation](https://docs.opencv.org/4.x/d5/dae/tutorial_aruco_detection.html) for dictionary selection, detection, and pose estimation.

## ID 0 assembly model

<img src="images/aruco_cell_assembly.png" alt="CAD view of the ID 0 cell with white hexagonal base and black marker insert" width="530">
