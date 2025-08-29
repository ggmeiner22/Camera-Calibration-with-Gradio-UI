# Camera Calibration (OpenCV + Gradio)

## Setup
- Open in Google Colab.
- Run the first cell to install packages.

## How to Use
1. Print the OpenCV chessboard: https://docs.opencv.org/4.x/pattern.png  
2. Capture 15–20 images of the board from varied angles.
3. In the notebook UI:
   - Upload `.jpeg` images → saved to `/content/images/`.
   - Set pattern size (inner corners) and square size (meters).
   - Click **Run Calibration**.
4. Results:
   - `calibration.json` storing K (intrinsics), R, t (extrinsics), D (distortion), width, height.
   - 3D camera pose plot.
   - Sample overlays with world axes.

## Code Structure
- **Calib**: calibration, I/O with OpenCV FileStorage.
- **Board**: chessboard object model.
- **Overlay**: draw axes overlays.
- **IO**: directory and file helpers.
- **Helper Functions**: These functions help save images with axes and before/after distortion.
- **Gradio UI**: Interface for UI

