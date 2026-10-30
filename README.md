# 3D Shape Classifier

A PointNet model for classifying scanned point clouds as spheres, cones, cubes, cylinders, or cuboids. Built with Python and PyTorch, with a web interface for uploading and visualizing scans.

## Features

- Point cloud normalization, sampling, and training augmentation.
- Model training with validation, early stopping, and checkpoint saving.
- Test-set evaluation with classification reports and confusion matrices.
- Interactive 3D visualization and shape prediction.

## Workflow

```mermaid
flowchart LR
    A["3D scan<br/>X, Y, Z coordinates"] --> B["Normalize & sample<br/>point cloud"]
    B --> C["PointNet<br/>feature extraction"]
    C --> D["Class scores"]
    D --> E["Predicted shape<br/>Sphere · Cone · Cube<br/>Cylinder · Cuboid"]
```

<details>
<summary>Training curves</summary>

![Training and validation loss and accuracy](assets/training_curves.png)

</details>

## Run

```bash
python -m pip install numpy torch scikit-learn seaborn matplotlib streamlit plotly
```

Train and evaluate:

```bash
python shape_classifier.py --data_dir ./data
```

Use `--mode train` or `--mode eval` to run either stage separately. Evaluation and the web app load `assets/model/best_model.pth`.

```bash
streamlit run app.py
```

## Data

Organize scans by split and class:

```text
data/
  train/<class>/*.TXT
  val/<class>/*.TXT
  test/<class>/*.TXT
```

Each file contains comma-separated X, Y, Z coordinates after three header lines. The loader normalizes each cloud and samples or pads it to a fixed point count.

Checkpoints, training curves, metrics, and evaluation reports are written to `assets/`.

[Related 3D scanner](https://github.com/lstrjessh/PID-Adaptive-Speed-Arduino-based-3D-Scanner-Using-an-IR-Analog-Distance-Sensor)
