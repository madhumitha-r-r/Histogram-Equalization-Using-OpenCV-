
# Histogram Equalization Using OpenCV (Grayscale and Color Images)

## Aim

To write a Python program using OpenCV to perform histogram equalization on grayscale and color images to enhance image contrast.

## Software Requirements

- Python 3
- Anaconda / Jupyter Notebook
- OpenCV
- NumPy
- Matplotlib

## Algorithm

1. Import the required libraries: OpenCV, NumPy, and Matplotlib.
2. Read the image `parrot.jpg` in grayscale mode.
3. Display the original grayscale image and plot its histogram.
4. Apply histogram equalization using `cv2.equalizeHist()`.
5. Display the original and enhanced grayscale images with their histograms.
6. Read the image in color mode.
7. Split the image into Blue, Green, and Red channels and plot their histograms.
8. Convert the image from BGR to HSV color space.
9. Apply histogram equalization to the Value (V) channel.
10. Merge the HSV channels and convert the image back to BGR format.
11. Display the original and enhanced color images with their histograms.
12. Save the enhanced color image as `enhanced_color.jpg`.

## Program

### 1. Grayscale Histogram Equalization

```python
import cv2
import matplotlib.pyplot as plt

gray = cv2.imread('parrot.jpg', 0)

if gray is None:
    print("Image not found. Check the file name and folder.")
else:
    plt.figure(figsize=(10, 8))

    plt.subplot(2, 2, 1)
    plt.imshow(gray, cmap='gray')
    plt.title('Original Grayscale Image')
    plt.axis('off')

    plt.subplot(2, 2, 2)
    plt.hist(gray.ravel(), 256, [0, 256], color='black')
    plt.title('Original Histogram')

    equalized = cv2.equalizeHist(gray)

    plt.subplot(2, 2, 3)
    plt.imshow(equalized, cmap='gray')
    plt.title('Enhanced Grayscale Image')
    plt.axis('off')

    plt.subplot(2, 2, 4)
    plt.hist(equalized.ravel(), 256, [0, 256], color='black')
    plt.title('Enhanced Histogram')

    plt.tight_layout()
    plt.show()
```

### 2. Color Image Histogram Equalization

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt

img = cv2.imread("parrot.jpg")

if img is None:
    print("Error: parrot.jpg not found!")
else:
    b, g, r = cv2.split(img)

    hsv = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)
    h, s, v = cv2.split(hsv)

    v_eq = cv2.equalizeHist(v)

    hsv_eq = cv2.merge((h, s, v_eq))
    enhanced = cv2.cvtColor(hsv_eq, cv2.COLOR_HSV2BGR)

    plt.figure(figsize=(12, 8))

    plt.subplot(2, 2, 1)
    plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
    plt.title("Original Color Image")
    plt.axis("off")

    plt.subplot(2, 2, 2)
    plt.hist(b.ravel(), 256, [0, 256],
             color="blue", alpha=0.5, label="Blue")
    plt.hist(g.ravel(), 256, [0, 256],
             color="green", alpha=0.5, label="Green")
    plt.hist(r.ravel(), 256, [0, 256],
             color="red", alpha=0.5, label="Red")
    plt.title("Original BGR Histograms")
    plt.xlabel("Pixel Intensity")
    plt.ylabel("Frequency")
    plt.legend()

    plt.subplot(2, 2, 3)
    plt.imshow(cv2.cvtColor(enhanced, cv2.COLOR_BGR2RGB))
    plt.title("Enhanced Color Image")
    plt.axis("off")

    plt.subplot(2, 2, 4)
    plt.hist(v_eq.ravel(), 256, [0, 256], color="purple")
    plt.title("Enhanced V Channel Histogram")
    plt.xlabel("Pixel Intensity")
    plt.ylabel("Frequency")

    plt.tight_layout()
    plt.show()

    cv2.imwrite("enhanced_color.jpg", enhanced)

    print("Color histogram equalization completed successfully!")
    print("Saved as enhanced_color.jpg")
```

## Output

### Grayscale Histogram Equalization

- The original grayscale image is displayed.
- The original grayscale histogram is plotted.
- The enhanced grayscale image is displayed.
- The equalized histogram shows the redistribution of pixel intensities.

<img width="935" height="720" alt="image" src="https://github.com/user-attachments/assets/a298dce2-a954-4bd2-8573-03c44a716bb7" />

### Color Image Histogram Equalization

- The original color image is displayed.
- The histograms of the Blue, Green, and Red channels are plotted.
- The enhanced color image is displayed.
- The enhanced V-channel histogram is plotted.
- The enhanced image is saved as `enhanced_color.jpg`.

<img width="1070" height="717" alt="image" src="https://github.com/user-attachments/assets/2ec5e5d9-a57b-40f7-8e46-c78c63afe6cf" />

## Result

Thus, histogram equalization was successfully performed on grayscale and color images using OpenCV. The technique redistributed pixel intensities to improve image contrast and visibility.
