
## Histogram Stretching

Histogram stretching, also known as contrast stretching, is a technique used in image processing to enhance the contrast of an image. This method works by expanding the range of intensity values in an image to cover the full range of possible values.

## Steps Involved

1. **Identify the Minimum and Maximum Intensity Values**: Determine the minimum (\(r_{min}\)) and maximum (\(r_{max}\)) intensity values in the original image.
2. **Apply the Stretching Transformation**: Use the following transformation to map the original intensity values to the new range:

   \[
   $s = \frac{(r - r_{min}) \cdot (L - 1)}{r_{max} - r_{min}}$
   \]

   where:
   - \( s \) is the new intensity value.
   - \( r \) is the original intensity value.
   - \( L \) is the number of possible intensity levels (e.g., 256 for an 8-bit image).

## Example

Given an image with intensity values ranging from \( r_{min} = 50 \) to \( r_{max} = 200 \), the histogram stretching process will map these values to the full range of 0 to 255.

## Python Implementation

Here's a simple implementation in Python:

```python
import cv2
import numpy as np

# Load the image
img = cv2.imread('image.jpg', 0)

# Find the minimum and maximum pixel values
r_min, r_max = np.min(img), np.max(img)

# Apply histogram stretching
stretched_img = ((img - r_min) / (r_max - r_min) * 255).astype(np.uint8)

# Display the results
cv2.imshow('Original Image', img)
cv2.imshow('Stretched Image', stretched_img)
cv2.waitKey(0)
cv2.destroyAllWindows()
