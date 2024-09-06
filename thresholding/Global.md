
### Global Thresholding


# Global Thresholding

## Explanation
Global thresholding uses a single threshold value for the entire image. It is a simple and fast method for converting a grayscale image into a binary image.

## Algorithm and Equations
1. **Thresholding Equation**:
   $$
   T(x, y) = \begin{cases} 
   0 & \text{if } I(x, y) \leq T \\
   255 & \text{if } I(x, y) > T 
   \end{cases}
   $$
   where \( T \) is the threshold value **given by the user or decided**.

## Pros and Cons
- **Pros**:
  - Simple and fast.
  - Easy to implement.
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

# Apply global thresholding
_, global_thresh_img = cv2.threshold(img, 127, 255, cv2.THRESH_BINARY)

# Display the results
plt.subplot(121), plt.imshow(img, cmap='gray'), plt.title('Original Image')
plt.subplot(122), plt.imshow(global_thresh_img, cmap='gray'), plt.title('Global Thresholding')
plt.show()
