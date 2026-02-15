# Circle Detection in Video Frames

This project uses OpenCV to detect circular objects (cans, balls, etc.) in video frames using the Hough Circle Transform. It processes each frame through a grayscale conversion, Gaussian blur, Canny edge detection, and circle detection pipeline. Detected circles are highlighted in green and displayed in real time. Processed frames are also written to an output video file.

## Features

- **Circle Detection:** Identifies circles in video frames using the Hough Circle Transform.
- **Real-Time Display:** Processes and displays each frame as circles are detected.
- **Video Output:** Saves the processed video with circle overlays to `OverlayVideo.mp4`.
- **Modular Structure:** Each processing step lives in its own module for easy adjustment and maintenance.

## Project Structure

```
VideoCanDetection/
├── main.py                   # Entry point — captures, processes, and releases video
├── CaptureVideo.py           # Loads video file via OpenCV VideoCapture
├── VideoProcess.py           # Main frame loop — processes, writes, and displays each frame
├── FrameProcessing.py        # Image processing pipeline (grayscale → blur → edge → detect → draw)
├── Grayscale.py              # Converts BGR frames to grayscale
├── GaussianBlur.py           # Applies Gaussian blur for noise reduction
├── CannyEdge.py              # Canny edge detection
├── HoughCircleDetection.py   # Hough Circle Transform detection
├── PutCircle.py              # Draws circles on frames
├── FrameOutput.py            # Displays frames in an OpenCV window
├── VideoWriting.py           # Initializes video writer and writes frames to output file
├── VideoReleasing.py         # Releases video resources and closes windows
└── canvideo.mp4              # Input video file
```

## How It Works

1. **Open Video File:** Reads `canvideo.mp4` frame by frame.
2. **Grayscale Conversion:** Each frame is converted to grayscale.
3. **Gaussian Blur:** A 15x15 Gaussian blur is applied to reduce noise.
4. **Edge Detection:** Canny edge detection extracts edges (thresholds: 5, 30).
5. **Circle Detection:** The Hough Circle Transform identifies circles in the edge map.
6. **Draw Circles:** Detected circles and their center points are drawn in green on the original frame.
7. **Output:** The annotated frame is displayed on screen and written to `OverlayVideo.mp4`.

## Usage

### Install Dependencies

```bash
pip install opencv-python numpy
```

### Prepare the Video File

Place your video file in the project directory. By default the program reads `canvideo.mp4`. To use a different file, update the `videoname` variable in `main.py`.

### Run the Program

```bash
python main.py
```

### Controls

- A window named "Output" displays the processed video in real time.
- Press **q** to stop processing early.
- The program exits automatically when all frames are processed.

### Output

The processed video with circle overlays is saved as `OverlayVideo.mp4` in the project directory.

## Functions

### main.py

Orchestrates the pipeline: captures the video, runs processing, and releases resources.

### CaptureVideo.py

- `CaptureVid(videoname)` — Opens a video file and returns a `cv2.VideoCapture` object.

### VideoProcess.py

- `VideoProcessing(video)` — Loops through each frame, processes it, writes it to the output file, and displays it. Returns the `VideoWriter` object.

### FrameProcessing.py

- `ImageProcess(frame)` — Runs the full processing pipeline on a single frame: grayscale, blur, edge detection, circle detection, and circle drawing. Returns the annotated frame.

### Grayscale.py

- `grayframe(frame)` — Converts a BGR image to grayscale.

### GaussianBlur.py

- `Gaussian(frame, dimension1, dimension2, sigma)` — Applies Gaussian blur with the given kernel size and sigma.

### CannyEdge.py

- `CannyDetection(frame, min, max)` — Runs Canny edge detection with the given thresholds.

### HoughCircleDetection.py

- `HoughCircle(frame, dp, distance, param1, param2, min, max)` — Detects circles using `cv2.HoughCircles` with `HOUGH_GRADIENT` method.

### PutCircle.py

- `puttingcircle(frame, x, y, radius, color, thickness)` — Draws a circle on the frame at the specified position.

### FrameOutput.py

- `OutputFrame(name, frame)` — Displays a frame in an OpenCV window with the given name.

### VideoWriting.py

- `initresult(filename, size)` — Creates a `VideoWriter` (mp4v codec, 10 FPS) for the given filename and frame size.
- `writeframe(frame, result)` — Writes a frame to the video writer.

### VideoReleasing.py

- `ReleaseVideo(video)` — Releases a video capture or writer object.
- `destroy()` — Closes all OpenCV windows.

## Requirements

- Python 3.x
- OpenCV (`opencv-python`)
- NumPy
