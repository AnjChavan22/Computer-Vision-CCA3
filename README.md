# Computer Vision CCA 3
### Image Processing · Feature Extraction · Object Detection · Motion Estimation

<p align="center">
  **Practical Coding Assignment – Units 3, 4 and 5**  
  Python | OpenCV | NumPy | Matplotlib | scikit-image | YOLOv8
</p>

---

## 1. Project Overview

This project demonstrates practical applications of Computer Vision using Python. It covers image restoration, image segmentation, feature extraction, object recognition, and motion estimation using photographs and a self-recorded video.

The objective is to understand how different computer vision algorithms work, implement them using Python libraries, and evaluate their outputs.

## 2. Objectives

- Apply noise removal and image restoration techniques.
- Perform image segmentation using thresholding and morphological operations.
- Extract and match image features using HOG and SIFT.
- Detect faces and objects using Viola–Jones and YOLO.
- Estimate motion using frame differencing, background subtraction, and optical flow.
- Compare the results of different computer vision techniques.

## 3. Dataset Description

The project uses two photographs and one self-recorded video.

| Input | Description | Dimensions / Details |
|---|---|---|
| `Image_1.jpg` | First input photograph | 1600 × 1068 pixels |
| `Image_2.jpg` | Second input photograph | 1600 × 1068 pixels |
| `Sample_video.mp4` | Self-recorded video for motion analysis | 30 FPS, 300 frames, 10 seconds |

## 4. Technologies Used

| Technology / Library | Purpose |
|---|---|
| Python | Main programming language |
| OpenCV | Image processing, segmentation, detection and motion analysis |
| NumPy | Numerical and array operations |
| Matplotlib | Image and result visualization |
| scikit-image | Image quality evaluation using PSNR and SSIM |
| Ultralytics YOLOv8 | Object detection |
| Google Colab | Development and execution environment |

---

# 5. Tasks Implemented

## Task 1 – Image Restoration and Segmentation

**Objective:** Add noise to an image, restore it using filtering techniques, evaluate image quality, and perform segmentation.

### Techniques Implemented

| Technique | Implementation |
|---|---|
| Gaussian Noise | Added Gaussian noise with mean 0 and standard deviation 25 |
| Salt-and-Pepper Noise | Added noise with probability 0.04 (4%) |
| Median Filtering | Applied a 5 × 5 median filter |
| Gaussian Filtering | Applied a 5 × 5 Gaussian filter |
| Thresholding | Used Otsu's thresholding method |
| Morphological Operations | Erosion, dilation, opening and closing |
| Edge Detection | Canny edge detection with thresholds 100 and 200 |
| Watershed | Marker-based image segmentation |

### Image Quality Evaluation

PSNR and SSIM were used to compare restored images with the original image.

| Noise Type | Filtering Method | PSNR (dB) | SSIM |
|---|---|---:|---:|
| Gaussian | Median Filter | 27.05 | 0.6543 |
| Gaussian | Gaussian Filter | 28.65 | 0.6977 |
| Salt-and-Pepper | Median Filter | 28.59 | 0.8949 |
| Salt-and-Pepper | Gaussian Filter | 26.69 | 0.6124 |

### Key Observations

- Gaussian filtering performed better for the tested Gaussian noise.
- Median filtering performed better for the tested Salt-and-Pepper noise.
- Otsu's method calculated an automatic threshold value of **79**.
- Watershed segmentation reported **4 foreground labels**.

---

## Task 2 – Feature Extraction and Matching

**Objective:** Extract important image features and identify matching points between two photographs.

### Techniques Implemented

| Technique | Description |
|---|---|
| HOG | Histogram of Oriented Gradients used to extract shape and gradient information |
| SIFT | Scale-Invariant Feature Transform used to detect keypoints and descriptors |
| Brute Force Matcher | Compared descriptors between the two images |
| Lowe's Ratio Test | Selected good matches using a ratio threshold of 0.75 |
| Image Rotation | Tested feature matching after 45° rotation |
| Image Resizing | Tested feature matching after resizing to 50% |

**HOG parameters:** 9 orientations, 8 × 8 pixels per cell and 2 × 2 cells per block.

### Results

| Measurement | Result |
|---|---:|
| HOG feature length – Image 1 | 945,648 |
| HOG feature length – Image 2 | 945,648 |
| SIFT keypoints – Image 1 | 4,051 |
| SIFT keypoints – Image 2 | 2,263 |
| Total matches | 4,051 |
| Good matches | 186 |
| Good matches after 45° rotation | 150 |
| Good matches after 50% resizing | 101 |

### Key Observations

- HOG extracted feature vectors from both photographs.
- SIFT identified keypoints and descriptors in the images.
- Feature matching was possible even after rotation and resizing.
- The number of good matches decreased after image transformations.

---

## Task 3 – Object Recognition

**Objective:** Detect faces and recognize objects in photographs and video frames.

### Techniques Implemented

| Algorithm | Purpose |
|---|---|
| Viola–Jones | Face detection using Haar Cascade classifiers |
| YOLOv8 Nano | Object detection using a pretrained deep learning model |

### Detection Results

| Method | Input | Detection | Confidence |
|---|---|---|---:|
| Viola–Jones | Photograph | 1 face | — |
| YOLOv8 Nano | Photograph | 1 person | 89.4% |
| YOLOv8 Nano | Selected middle video frame | 1 sports ball | 29.3% |

**YOLO model:** `yolov8n.pt`  
**Confidence threshold:** 0.25

### Key Observations

- Viola–Jones successfully detected one face.
- YOLOv8 detected one person in the photograph.
- YOLOv8 detected one sports ball in the selected video frame.
- The sports ball detection had relatively low confidence, so it should be interpreted cautiously.

*Note: YOLO detection on the video was demonstrated using one selected middle frame, not continuous detection across all frames.*

---

## Task 4 – Motion Estimation

**Objective:** Analyse movement and changes between video frames using different motion estimation techniques.

### Techniques Implemented

| Technique | Description |
|---|---|
| Frame Differencing | Identifies changes by comparing two video frames |
| MOG2 Background Subtraction | Separates foreground objects from the background |
| Lucas–Kanade Optical Flow | Tracks selected feature points between consecutive frames |

### Parameters Used

| Technique | Parameters |
|---|---|
| Frame Differencing | Frames 0 and 15, Gaussian blur 5 × 5, threshold 15 |
| MOG2 | History = 100, Variance Threshold = 25, Shadow Detection = True |
| Lucas–Kanade | Shi–Tomasi feature selection and consecutive-frame tracking |

### Results

| Measurement | Result |
|---|---:|
| Video frame rate | 30 FPS |
| Total frames | 300 |
| Video duration | 10 seconds |
| Frames processed using MOG2 | 300 |
| Feature points detected | 42 |
| Feature points successfully tracked | 42 |
| Tracking success rate | 100% |

### Key Observations

- Frame differencing highlighted pixel changes between selected frames.
- MOG2 processed all 300 frames to identify foreground regions.
- Lucas–Kanade successfully tracked all 42 selected feature points between consecutive frames.

---

# 6. Overall Results and Comparison

| Task | Main Techniques | Important Result |
|---|---|---|
| Image Restoration and Segmentation | Median, Gaussian, Otsu, Morphology, Canny, Watershed | Best tested Gaussian-noise result: 28.65 dB PSNR |
| Feature Extraction and Matching | HOG, SIFT, Brute Force Matcher | 186 good matches between the original photographs |
| Object Recognition | Viola–Jones, YOLOv8 | One face and one person detected in the photograph |
| Motion Estimation | Frame Differencing, MOG2, Lucas–Kanade | 42 out of 42 feature points tracked |

## 7. Project Structure

A suggested GitHub repository structure is:

```text
Computer-Vision-CCA3/
│
├── Computer_Vision_CCA3.ipynb
│
├── dataset/
│   ├── original.jpg
│   ├── second.jpg
│   └── original_video.mp4
│
├── outputs/
│   ├── task1_image_restoration/
│   ├── task2_feature_matching/
│   ├── task3_object_detection/
│   └── task4_motion_estimation/
│
├── README.md
└── requirements.txt
```

*The folder names above are a suggested organization. Adjust them to match the files actually included in your repository.*

## 8. How to Run the Project

The notebook was developed and executed using Google Colab.

1. Download or clone the project repository.
2. Open [Google Colab](https://colab.research.google.com/).
3. Upload `Computer_Vision_CCA3.ipynb`.
4. Upload the required photographs and video when prompted by the notebook.
5. Install any missing dependencies using the notebook's installation cell.
6. Run the notebook cells in sequence.
7. Review the generated output images, visualizations and results.

### Install Required Libraries

```bash
pip install opencv-python numpy matplotlib scikit-image ultralytics
```

## 9. Video Presentation Guide

The project explanation video should cover the following points:

| No. | Presentation Section | What to Explain |
|---:|---|---|
| 1 | Introduction | Introduce the project and its objectives |
| 2 | Dataset | Describe the two photographs and the self-recorded video |
| 3 | Algorithms | Explain the techniques implemented in all four tasks |
| 4 | Source Code | Demonstrate the important code sections in the notebook |
| 5 | Results | Show the important input and output images and detection results |
| 6 | Comparison | Compare the techniques and explain the observations |

Explain the implementation and results in your own words.

## 10. Conclusion

This project provided practical experience with different computer vision techniques using Python. It covered image restoration, segmentation, feature extraction, feature matching, object recognition and motion estimation.

The experiments demonstrated that different algorithms are suitable for different tasks. For example, Gaussian filtering performed better for the tested Gaussian noise, while median filtering was more effective for Salt-and-Pepper noise. SIFT enabled feature matching after image transformations, YOLOv8 performed object detection, and Lucas–Kanade successfully tracked selected feature points.

Overall, the assignment helped develop an understanding of computer vision concepts and their practical applications.

## 11. References

- [OpenCV Documentation](https://docs.opencv.org/)
- [NumPy Documentation](https://numpy.org/doc/)
- [Matplotlib Documentation](https://matplotlib.org/stable/)
- [scikit-image Documentation](https://scikit-image.org/docs/stable/)
- [Ultralytics YOLO Documentation](https://docs.ultralytics.com/)

---



<p align="center">
  **Computer Vision CCA 3**  
  *Image Processing • Feature Extraction • Object Recognition • Motion Estimation*
</p>
