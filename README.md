# Camera-Calibration-with-Gradio-UI

Calibrate a camera from chessboard photos and visualize results in a simple Gradio UI (inline in Colab).

## Features
- Upload chessboard calibration images
- Automatic corner detection
- Compute intrinsics (K) & distortion (D)
- 3D camera pose visualization
- Undistortion preview (before/after)
- Export results to `calibration.json`

## Installation

```bash
git clone https://github.com/ggmeiner22/Camera-Calibration-with-Gradio-UI.git
cd Camera-Calibration-with-Gradio-UI
pip install -r requirements.txt
```

Dependencies include: `opencv-python`, `numpy`, `gradio`, `plotly`, `pillow`, `pytransform3d`.

## Usage

### Run locally
```bash
python app.py
```

Gradio will show a local link (e.g. `http://127.0.0.1:7860`). Open it in your browser.

### In notebooks (Colab/Jupyter)
```python
!pip install opencv-python numpy gradio plotly pillow pytransform3d
from app import demo
demo.launch(inline=True)
```

## Preparing Calibration Photos
- Use 15–20 clear chessboard images from varied angles
- Ensure sharp focus, consistent lighting
- **Inner corners (cols/rows):** e.g. 9×6 for a 10×7 board
- **Square size:** 0.0217714286 m (≈ 21.77 mm)

## Output
- `calibration.json` with:
  - Intrinsics `K`
  - Distortion coefficients `D`
  - Extrinsics (`rvecs`, `tvecs`)
  - Image resolution
- 3D camera poses plot
- Overlay images with axes
- Undistortion preview (before/after)

## License
MIT © 2025 Garrett Gmeiner

