
# Automatic Thresholding

## Explanation
Iterative thresholding is a method where the threshold value is iteratively updated based on the mean of the foreground and background pixels until convergence. This method can improve thresholding results by refining the threshold value.

## Algorithm and Equations
1. **Initial Threshold**:
   $$
   T_0 = \frac{\text{max}(I) + \text{min}(I)}{2}
   $$

2. **Update Threshold**:
   $$
   T_{n+1} = \frac{\mu_1 + \mu_2}{2}
   $$
   where \( \mu_1 \) and \( \mu_2 \) are the means of the foreground and background pixels, respectively.

## Pros and Cons
- **Pros**:
  - Can improve thresholding results.
  - Iteratively refines the threshold value.
- **Cons**:
  - Requires multiple iterations.
  - Computationally intensive.

## When to Use
- Use when you need to refine the threshold value for better segmentation results.

## Sample Code Implementation

Here's a simple implementation in Python using OpenCV:

```python
import cv2
import numpy as np
from matplotlib import pyplot as plt

# Load the image
img = cv2.imread('image.jpg', 0)

# Initial threshold
T = (np.max(img) + np.min(img)) / 2

# Iterative thresholding
while True:
    foreground = img[img > T]
    background = img[img <= T]
    
    new_T = (np.mean(foreground) + np.mean(background)) / 2
    
    if abs(new_T - T) < 1:
        break
    
    T = new_T

# Apply the final threshold
_, iterative_thresh_img = cv2.threshold(img, T, 255, cv2.THRESH_BINARY)

# Display the results
plt.subplot(121), plt.imshow(img, cmap='gray'), plt.title('Original Image')
plt.subplot(122), plt.imshow(iterative_thresh_img, cmap='gray'), plt.title('Iterative Thresholding')
plt.show()
