# EX. NO. 03

# HISTOGRAM EQUALIZATION USING OPENCV (GRAYSCALE & COLOR IMAGES)

## AIM

To write a Python program using OpenCV to perform histogram equalization on grayscale and color images to improve image contrast and intensity distribution.

The program performs the following operations:

- Read and display a grayscale image.
- Plot the histogram of the grayscale image.
- Apply histogram equalization to the grayscale image.
- Read and display a color image.
- Plot the histograms of the Blue, Green, and Red channels.
- Convert the color image from BGR to HSV color space.
- Apply histogram equalization to the Value (V) channel.
- Convert the enhanced image back to BGR format.
- Display the original and enhanced images with their histograms.

## SOFTWARE REQUIRED

1. Anaconda – Python
2. Jupyter Notebook / VS Code
3. OpenCV (`cv2`)
4. NumPy
5. Matplotlib

## ALGORITHM

### Grayscale Image

1. Import OpenCV, NumPy, and Matplotlib.
2. Read `parrot.jpg` in grayscale mode.
3. Check whether the image is loaded successfully.
4. Display the original grayscale image and plot its histogram.
5. Apply histogram equalization using `cv2.equalizeHist()`.
6. Display the enhanced grayscale image and its histogram.

### Color Image

1. Read `parrot.jpg` in color mode.
2. Check whether the image is loaded successfully.
3. Split the image into Blue, Green, and Red channels and plot their histograms.
4. Convert the image from BGR to HSV color space.
5. Split the HSV image into Hue, Saturation, and Value channels.
6. Apply histogram equalization to the Value channel.
7. Merge the HSV channels and convert the result back to BGR.
8. Display the original color image and its BGR channel histograms.
9. Display the enhanced color image and its BGR channel histograms.

## PROGRAM

### Developed By

**Name:** Mohammed Ameer F
### Register Number
212225040248

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt

# Read the image in grayscale
gray = cv2.imread("parrot.jpg", cv2.IMREAD_GRAYSCALE)

if gray is None:
    raise FileNotFoundError("Error: parrot.jpg not found!")

# Apply histogram equalization to grayscale image
equalized_gray = cv2.equalizeHist(gray)

# Display grayscale image and histograms
plt.figure(figsize=(10, 8))

plt.subplot(2, 2, 1)
plt.imshow(gray, cmap="gray")
plt.title("Original Grayscale Image")
plt.axis("off")

plt.subplot(2, 2, 2)
plt.hist(gray.ravel(), 256, [0, 256], color="gray")
plt.title("Original Grayscale Histogram")
plt.xlabel("Pixel Intensity")
plt.ylabel("Frequency")

plt.subplot(2, 2, 3)
plt.imshow(equalized_gray, cmap="gray")
plt.title("Equalized Grayscale Image")
plt.axis("off")

plt.subplot(2, 2, 4)
plt.hist(equalized_gray.ravel(), 256, [0, 256], color="gray")
plt.title("Equalized Grayscale Histogram")
plt.xlabel("Pixel Intensity")
plt.ylabel("Frequency")

plt.tight_layout()
plt.show()

# Read the image in color
color = cv2.imread("parrot.jpg")

if color is None:
    raise FileNotFoundError("Error: parrot.jpg not found!")

# Convert BGR image to RGB for Matplotlib display
color_rgb = cv2.cvtColor(color, cv2.COLOR_BGR2RGB)

# Convert BGR image to HSV
hsv = cv2.cvtColor(color, cv2.COLOR_BGR2HSV)

# Split HSV channels
h, s, v = cv2.split(hsv)

# Apply histogram equalization to the Value channel
equalized_v = cv2.equalizeHist(v)

# Merge HSV channels and convert back to BGR
equalized_hsv = cv2.merge((h, s, equalized_v))
equalized_color = cv2.cvtColor(equalized_hsv, cv2.COLOR_HSV2BGR)

# Convert enhanced image to RGB for Matplotlib
equalized_color_rgb = cv2.cvtColor(
    equalized_color, cv2.COLOR_BGR2RGB
)

# Display original color image and BGR channel histograms
plt.figure(figsize=(10, 8))

plt.subplot(2, 2, 1)
plt.imshow(color_rgb)
plt.title("Original Color Image")
plt.axis("off")

plt.subplot(2, 2, 2)
for channel, color_name, label in [
    (0, "blue", "Blue"),
    (1, "green", "Green"),
    (2, "red", "Red")
]:
    histogram = cv2.calcHist([color], [channel], None, [256], [0, 256])
    plt.plot(histogram, color=color_name, label=label)

plt.title("Original BGR Channel Histograms")
plt.xlabel("Pixel Intensity")
plt.ylabel("Frequency")
plt.legend()

plt.subplot(2, 2, 3)
plt.imshow(equalized_color_rgb)
plt.title("Enhanced Color Image (HSV)")
plt.axis("off")

plt.subplot(2, 2, 4)
for channel, color_name, label in [
    (0, "blue", "Blue"),
    (1, "green", "Green"),
    (2, "red", "Red")
]:
    histogram = cv2.calcHist(
        [equalized_color], [channel], None, [256], [0, 256]
    )
    plt.plot(histogram, color=color_name, label=label)

plt.title("Enhanced BGR Channel Histograms")
plt.xlabel("Pixel Intensity")
plt.ylabel("Frequency")
plt.legend()

plt.tight_layout()
plt.show()
```

## OUTPUT

### i) Grayscale Histogram Equalization

- Original grayscale image is displayed.
- Histogram of the original grayscale image is plotted.
- Equalized grayscale image is displayed.
- Histogram of the equalized grayscale image is plotted.

### ii) Color Image Histogram Equalization

- Original color image is displayed.
- Histograms of the Blue, Green, and Red channels are plotted.
- Enhanced color image after equalization of the HSV Value channel is displayed.
- Histograms of the enhanced image's Blue, Green, and Red channels are plotted.

## RESULT

Thus, histogram equalization is performed on grayscale and color images using OpenCV. The grayscale image is enhanced using `cv2.equalizeHist()`, and the color image is enhanced by equalizing the Value (V) channel in HSV color space. This improves the distribution of image intensities and can enhance image contrast.
