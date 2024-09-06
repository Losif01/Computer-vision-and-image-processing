
# Local Thresholding

## Explanation
Local thresholding calculates the threshold for small regions of the image, allowing for better handling of varying lighting conditions. It adjusts the threshold value dynamically based on local statistics like mean and standard deviation.

## Algorithm and Equations
1. **Thresholding Equation**:
   $$
   T(x, y) = \frac{1}{N} \sum_{(i,j) \in \text{Neighborhood}} I(i, j)
   $$

## Pros and Cons
- **Pros**:
  - Effective for images with local variations in illumination.
  - Can handle complex lighting conditions.
- **Cons**:
  - Computationally intensive.
  - May require tuning of parameters.

## When to Use
- Use when the image has local variations in lighting or shadows.

## Sample Code Implementation

Here's a simple implementation in Python using OpenCV:

```python
import cv2
import numpy as np
from matplotlib import pyplot as plt

# Load the image
img = cv2.imread('image.jpg', 0)

# Apply local thresholding
local_thresh_img = cv2.adaptiveThreshold(img, 255, cv2.ADAPTIVE_THRESH_MEAN_C, cv2.THRESH_BINARY, 11, 2)

# Display the results
plt.subplot(121), plt.imshow(img, cmap='gray'), plt.title('Original Image')
plt.subplot(122), plt.imshow(local_thresh_img, cmap='gray'), plt.title('Local Thresholding')
plt.show()
