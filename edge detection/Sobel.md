# Sobel Operator

The Sobel operator is a popular edge detection algorithm used in image processing and computer vision. It works by calculating the gradient of the image intensity at each pixel, which helps to highlight regions of high spatial frequency that correspond to edges.

## How It Works

The Sobel operator uses two 3x3 convolution kernels, one for detecting changes in the horizontal direction (Gx) and one for detecting changes in the vertical direction (Gy). These kernels are applied to the image to approximate the gradient.

### Sobel Kernels

- **Horizontal Kernel ($G_x$)**:
  $$
  G_x = \begin{bmatrix}
  -1 & 0 & 1 \\
  -2 & 0 & 2 \\
  -1 & 0 & 1
  \end{bmatrix}
  $$

- **Vertical Kernel ($G_y$)**:
  $$
  G_y = \begin{bmatrix}
  -1 & -2 & -1 \\
  0 & 0 & 0 \\
  1 & 2 & 1
  \end{bmatrix}
  $$

### Gradient Calculation

The gradient magnitude and direction are calculated as follows:

- **Gradient Magnitude**:
  $$
  G = \sqrt{G_x^2 + G_y^2}
  $$

- **Gradient Direction**:
  $$
  \theta = \arctan\left(\frac{G_y}{G_x}\right)
  $$

## Example

Let's consider an example where we apply the Sobel operator to an image to detect edges.

### Python Implementation

Here's a simple implementation in Python using OpenCV:

```python
import cv2
import numpy as np
from matplotlib import pyplot as plt

# Load the image
img = cv2.imread('image.jpg', 0)

# Apply Sobel operator
sobel_x = cv2.Sobel(img, cv2.CV_64F, 1, 0, ksize=3)
sobel_y = cv2.Sobel(img, cv2.CV_64F, 0, 1, ksize=3)

# Calculate the gradient magnitude
sobel_magnitude = np.sqrt(sobel_x**2 + sobel_y**2)

# Display the results
plt.subplot(131), plt.imshow(img, cmap='gray'), plt.title('Original Image')
plt.subplot(132), plt.imshow(sobel_x, cmap='gray'), plt.title('Sobel X')
plt.subplot(133), plt.imshow(sobel_y, cmap='gray'), plt.title('Sobel Y')
plt.figure()
plt.imshow(sobel_magnitude, cmap='gray'), plt.title('Gradient Magnitude')
plt.show()
