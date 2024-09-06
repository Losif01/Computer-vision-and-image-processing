# Simple Thresholding

## Explanation
Simple thresholding is a basic technique in image processing where each pixel in a grayscale image is converted to either black or white based on a fixed threshold value. If the pixel intensity is greater than the threshold, it is set to white; otherwise, it is set to black.

## Algorithm and Equations
1. **Thresholding Equation**:
   $$
   T(x, y) = \begin{cases} 
   0 & \text{if } I(x, y) \leq T \\
   255 & \text{if } I(x, y) > T 
   \end{cases}
   $$
   where \( I(x, y) \) is the intensity of the pixel at position \($(x, y)$\) and \( T \) is the threshold value.

## Pros and Cons
- **Pros**:
  - Simple and easy to implement.
  - Fast and computationally efficient.
- **Cons**:
  - Ineffective for images with varying lighting conditions.
  - Can result in loss of important details.

## When to Use
- Use when the image has uniform lighting and clear contrast between objects and background.

## Sample Code Implementation

Here's a simple implementation in Python using OpenCV:

```python
import cv2
import numpy as np
from matplotlib import pyplot as plt

# Load the image
img = cv2.imread('image.jpg', 0)

# Apply simple thresholding
_, thresh_img = cv2.threshold(img, 127, 255, cv2.THRESH_BINARY)

# Display the results
plt.subplot(121), plt.imshow(img, cmap='gray'), plt.title('Original Image')
plt.subplot(122), plt.imshow(thresh_img, cmap='gray'), plt.title('Thresholded Image')
plt.show()
