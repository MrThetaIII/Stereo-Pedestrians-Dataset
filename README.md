# Stereo Pedestrian Dataset - Skeletal Tracking Dataset

A synthetic multi-view dataset for pedestrian skeletal map detection and localization using stereo camera triangulation.

## Dataset Overview

This dataset contains synchronized stereo camera footage of pedestrians in various urban scenarios, with ground truth 3D skeletal joint positions. It is designed for research in multi-view pedestrian tracking, pose estimation, and 3D localization.

### Statistics
- **Total Scenes**: 7
- **Total Frames**: 973
- **Camera Views**: 2 (Left and Right)
- **Characters**: 6 unique pedestrians (Remy, Josh, Lily, Alen, Jack, Marten)
- **Skeletal Joints**: 12 body parts per character

### Scenes

| Scene | Description | Frames | Characters |
|-------|-------------|--------|------------|
| Scene 0 | One Person | 104 | 1 (Remy) |
| Scene 1 | Crossing | 276 | 3 (Josh, Lily, Remy) |
| Scene 2 | Pedestrian Bridge | 103 | 3 (Josh, Lily, Remy) |
| Scene 3 | Busy Streets | 93 | 6 (All characters) |
| Scene 4 | Side way | 128 | 2 (Lily, Remy) |
| Scene 4a | Dawn | 129 | 2 (Lily, Remy) |
| Scene 4b | Night | 140 | 2 (Lily, Remy) |

**Note**: Scenes 4, 4a, and 4b share the same setting under different lighting conditions (daytime, dawn, and night).

## Dataset Structure
```txt
└── Scenes/
    └── Scene [0-4b]/
        ├── Left/                          # Left camera images
        │   └── frame#####.png
        ├── Right/                         # Right camera images
        │   └── frame#####.png
        ├── Characters/
        │   └── [Character_Name]/
        │       ├── CamLeft.csv           # 2D projections (left camera)
        │       ├── CamRight.csv          # 2D projections (right camera)
        │       └── World.csv             # 3D world coordinates
        ├── camera_data_per_frame.csv     # Frame-by-frame camera parameters
        ├── camera_intrinsics.txt         # Camera intrinsic parameters
        ├── camera_left_params.json       # Left camera extrinsics
        ├── camera_right_params.json      # Right camera extrinsics
        └── distillation_summary.txt      # Scene metadata
```

## Data Format

### Skeletal Joint Positions

Each character has three CSV files containing skeletal joint positions across frames:

#### Columns (12 body parts × 3 coordinates = 36 columns):
- **Arms**: RightArm, LeftArm (shoulder positions)
- **Forearms**: RightForeArm, LeftForeArm (elbow positions)
- **Hands**: RightHand, LeftHand (wrist positions)
- **Upper Legs**: RightUpLeg, LeftUpLeg (hip positions)
- **Lower Legs**: RightLeg, LeftLeg (knee positions)
- **Feet**: RightFoot, LeftFoot (ankle positions)

Each body part has X, Y, Z coordinates.

**Note**: Joint names represent the origin/base of each body part (e.g., "RightArm" refers to the shoulder position, "RightForeArm" refers to the elbow position, etc.).

#### Coordinate Systems:
- **World.csv**: 3D coordinates in world space
- **CamLeft.csv**: 2D projections in left camera image space (X, Y) + depth (Z, same as world Z)
- **CamRight.csv**: 2D projections in right camera image space (X, Y) + depth (Z, same as world Z)

### Camera Parameters

- **camera_intrinsics.txt**: Focal length, principal point, FOV
- **camera_left_params.json** / **camera_right_params.json**: Rotation matrices, translation vectors, and extrinsic parameters
- **camera_data_per_frame.csv**: Time-varying camera parameters (if applicable)

### Images

- Format: PNG
- Naming: `frame#####.png` (zero-padded 5-digit frame numbers)
- Synchronized stereo pairs for each frame

## Dataset Generation

This dataset was synthetically generated using **Unity Engine** with the following assets:

### Character Models
- **Mixamo**: Rigged and animated character models [https://www.mixamo.com/](https://www.mixamo.com/)
  - Provides realistic human animations and skeletal structures
  - Characters: Remy, Josh, Lily, Alen, Jack, Marten

### Environment
- **Japanese Otaku City**: Urban environment asset by Zenrin [https://www.zenrin.co.jp/contents/product/service/3d/asset/index.html](https://www.zenrin.co.jp/contents/product/service/3d/asset/index.html)
  - Realistic urban Japanese cityscape
  - Various urban scenarios including streets, crossings, and pedestrian bridges

The synthetic nature of the dataset provides:
- Perfect ground truth skeletal positions
- Precise camera calibration
- Control over lighting conditions and scene complexity
- Synchronized multi-view captures

## Use Cases

This dataset is suitable for:

1. **Multi-view pedestrian tracking**
2. **3D pose estimation from stereo cameras**
3. **Triangulation algorithm development and evaluation**
4. **Occlusion handling in crowded scenes**
5. **Lighting variation robustness testing** (Scene 4, 4a, 4b)
6. **Pedestrian re-identification across views**

## Acknowledgments

This dataset was created using:
- Character models from Mixamo (https://www.mixamo.com/)
- Japanese Otaku City environment asset by Zenrin (https://www.zenrin.co.jp/contents/product/service/3d/asset/index.html)
- Unity Engine for scene generation and rendering