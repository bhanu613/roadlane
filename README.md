# roadlane
Problem: detect lane lines in road video using classical computer vision.

Pipeline:

Grayscale conversion.

Canny edge detection.

Triangular region of interest mask.

HoughLinesP to extract line segments.

Overlay green lines on original frame.

How to run:

pip install -r requirements.txt.

python src/detector.py in a local environment with GUI support.

![image](https://user-images.githubusercontent.com/57340784/206966352-b78ed02b-8185-4320-a74d-4e7f269d4e9f.png)

![image](https://user-images.githubusercontent.com/57340784/205434216-d103889b-d101-494e-b99a-605eb472693b.png)
