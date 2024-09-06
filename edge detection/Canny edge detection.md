
# Adaptive Canny Edge Detection in Image Processing

Adaptive Canny edge detection is an enhancement of the traditional Canny edge detection algorithm. It automatically determines the optimal threshold values for edge detection, making it more robust to varying lighting conditions and image content.

## How Adaptive Canny Edge Detection Works

1. **Gaussian Smoothing:**
    - The image is smoothed using a Gaussian filter to reduce noise.
2. **Gradient Calculation:**
    - The gradient intensity and direction are calculated using the Sobel operator.
3. **Non-Maximum Suppression:**
    - Non-maximum suppression is applied to thin the edges.
4. **Adaptive Thresholding:**
    - Instead of using fixed thresholds, adaptive Canny calculates the thresholds based on the median of the pixel intensities.
5. **Edge Tracking by Hysteresis:**
    - Weak edges that are connected to strong edges are retained, while others are discarded.

## Sample Code

Here's a Python example using OpenCV to perform adaptive Canny edge detection:

```python
import cv2
import numpy as np

def auto_canny(image, sigma=0.33):
    # Compute the median of the single channel pixel intensities
    v = np.median(image)
    
    # Apply automatic Canny edge detection using the computed median
    lower = int(max(0, (1.0 - sigma) * v))
    upper = int(min(255, (1.0 + sigma) * v))
    edged = cv2.Canny(image, lower, upper)
    
    return edged

# Load the image
image = cv2.imread('input.jpg', cv2.IMREAD_GRAYSCALE)

# Apply adaptive Canny edge detection
edges = auto_canny(image)

# Save the result
cv2.imwrite('edges.jpg', edges)

# Display the result
cv2.imshow('Adaptive Canny Edge Detection', edges)
cv2.waitKey(0)
cv2.destroyAllWindows()
