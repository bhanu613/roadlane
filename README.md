# Road Lane Detection

## Problem

Detect lane lines in a road video using classical computer vision techniques (no deep learning), as a prototype for simple driver-assistance.

## Pipeline

- Convert each frame to grayscale.
- Apply Canny edge detection to highlight strong edges.
- Mask a triangular region of interest focused on the road surface.
- Use `cv2.HoughLinesP` to extract line segments corresponding to lane markings.
- Draw the detected lane lines in green and overlay them on the original frame.

## Results

The script processes `test.mp4` frame by frame and displays an output video where the lane lines are highlighted in green:

![IDE view](https://user-images.githubusercontent.com/57340784/206966352-b78ed02b-8185-4320-a74d-4e7f269d4e9f.png)

![Lane detection output](https://user-images.githubusercontent.com/57340784/205434216-d103889b-d101-494e-b99a-605eb472693b.png)

## How to Run

### Local setup

```bash
python -m venv venv
source venv/bin/activate  # on Windows: venv\Scripts\activate

pip install -r requirements.txt

python src/detector.py
```

Make sure you run this in an environment with GUI support so `cv2.imshow` windows can open.

### Run in Google Colab (no GUI)

You can also run the demo in a notebook environment without GUI windows:

1. Open a new Colab notebook.
2. Clone the repo and install dependencies:

   ```python
   !git clone https://github.com/yourusername/roadlane.git
   %cd roadlane
   !pip install -r requirements.txt
   ```

3. Run lane detection on the sample video and write the processed frames to `output.mp4`:

   ```python
   import cv2
   from src.detector import process

   cap = cv2.VideoCapture('data/test.mp4')

   ret, frame = cap.read()
   if not ret:
       raise RuntimeError("Cannot read first frame from data/test.mp4")

   height, width = frame.shape[:2]
   fourcc = cv2.VideoWriter_fourcc(*"mp4v")
   out = cv2.VideoWriter("output.mp4", fourcc, 20.0, (width, height))

   out.write(process(frame))

   while cap.isOpened():
       ret, frame = cap.read()
       if not ret:
           break
       out.write(process(frame))

   cap.release()
   out.release()
   ```

4. Download or display the video:

   ```python
   from IPython.display import Video
   Video("output.mp4", embed=True)
   ```

### Project structure

- `src/detector.py` – main lane detection script.
- `data/test.mp4` – sample road video used for the demo.
- `requirements.txt` – Python dependencies (`numpy`, `opencv-python`, `matplotlib`).
