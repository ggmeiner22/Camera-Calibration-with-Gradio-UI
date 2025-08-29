# Camera-Calibration-with-Gradio-UI

Calibrate a camera from chessboard photos and visualize results in a simple Gradio UI (inline in Colab).

## ✅ Features
- Upload `.jpeg` calibration images into `/content/images/`
- Run OpenCV calibration (intrinsics, distortion)
- Save results to `calibration.json`
- 3D plot of camera poses (Plotly)
- Image overlays with world axes
- Undistortion preview (before/after)

## Setup (Google Colab)
1. Open the notebook in **Google Colab**.
2. Run the first cell to install packages:
   ```bash
   %pip install opencv-python-headless numpy gradio plotly pytransform3d==3.3.0
