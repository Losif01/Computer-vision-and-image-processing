
## Histogram Equalization

Histogram equalization is a technique in image processing used to improve the contrast of an image. This method works by effectively spreading out the most frequent intensity values, which enhances the global contrast of the image.

## Steps Involved

1. **Compute the Histogram**: Calculate the histogram of the image, which is a distribution of the intensity levels.
2. **Compute the Cumulative Distribution Function (CDF)**: The CDF is calculated from the histogram.
3. **Normalize the CDF**: Normalize the CDF to scale it to the range of the intensity values.
4. **Map the Intensity Values**: Use the normalized CDF to map the old intensity values to new ones.

## Equations

1. **Histogram Calculation**:
   $$
   h(r_k) = n_k
   $$
   where \( $r_k$ \) is the \( k \)-th intensity level and \( $n_k$ \) is the number of pixels with intensity \( $r_k$ \).

2. **Probability Density Function (PDF)**:
   $$
   p(r_k) = \frac{n_k}{MN}
   $$
   where \( M \) and \( N \) are the dimensions of the image.

3. **Cumulative Distribution Function (CDF)**:
   \
$$cdf(r_k) = \sum_{j=0}^{k} p(r_j)$$
   \

4. **Normalization**:
   $$
   s_k = (L-1) \cdot cdf(r_k)
   $$
   where \( L \) is the number of possible intensity levels (e.g., 256 for an 8-bit image).

## Example

Given an image with intensity levels ranging from 0 to 255, the histogram equalization process will map the pixel values to new values based on the normalized CDF, thereby enhancing the contrast of the image.



## Python Implementation

Here's a simple implementation in Python:

```python
import cv2
import numpy as np
from matplotlib import pyplot as plt

# Load the image
img = cv2.imread('image.jpg', 0)

# Apply histogram equalization
equ = cv2.equalizeHist(img)

# Display the results
plt.subplot(121), plt.imshow(img, cmap='gray'), plt.title('Original Image')
plt.subplot(122), plt.imshow(equ, cmap='gray'), plt.title('Equalized Image')
plt.show()
