


# Color Thresholding

## Explanation
Color thresholding applies thresholding to color images by considering each color channel separately. This technique is useful for segmenting objects based on their color information.

## Algorithm and Equations
1. **Thresholding Equation**:
   $$
   T(x, y) = \begin{cases} 
   0 & \text{if } I_c(x, y) \leq T_c \\
   255 & \text{if } I_c(x, y) > T_c 
   \end{cases}
   $$
   where \( $I_c(x, y)$ \) is the intensity of the color channel \( c \) at position \($(x, y)$\) and \($T_c$ \) is the threshold value for channel \( $c$ \).

## Pros and Cons
- **Pros**:
  - Effective for color images.
  - Can separate objects based on color information.
- **Cons**:
  - More complex due to multiple channels.
  - Requires careful selection of color space and thresholds.

## When to Use
- Use when working with color images and need to segment based on color.

## Sample Code Implementation

Here's a simple implementation in Python using OpenCV:

```python
import cv2
import numpy as np
from matplotlib import pyplot as plt

# Load the image
img = cv2.imread('image.jpg')

# Convert to HSV color space
hsv = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)

# Define range of color to threshold
lower_color = np.array([30, 100, 100])
upper_color = np.array([90, 255, 255])

# Apply color thresholding
mask = cv2.inRange(hsv, lower_color, upper_color)
result = cv2.bitwise_and(img, img, mask=mask)

# Display the results
plt.subplot(131), plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB)), plt.title('Original Image')
plt.subplot(132), plt.imshow(mask, cmap='gray'), plt.title('Mask')
plt.subplot(133), plt.imshow(cv2.cvtColor(result, cv2.COLOR_BGR2RGB)), plt.title('Result')
plt.show()
