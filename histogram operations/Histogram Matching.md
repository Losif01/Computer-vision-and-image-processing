
# Histogram Matching

Histogram matching, also known as histogram specification, is a technique in image processing used to transform the histogram of an input image to match a specified histogram. This is useful for normalizing images taken under different lighting conditions or with different sensors.

## Steps Involved

1. **Compute the Histogram and CDF of the Input Image**: Calculate the histogram and cumulative distribution function (CDF) of the input image.
2. **Compute the Histogram and CDF of the Reference Image**: Calculate the histogram and CDF of the reference image.
3. **Create a Mapping Function**: Map the CDF of the input image to the CDF of the reference image.
4. **Apply the Mapping Function**: Transform the pixel values of the input image using the mapping function.

## Equations

1. **Histogram Calculation**:
   \[
   $h(r_k) = n_k$
   \]
   where \( $r_k$ \) is the \( $k$ \)-th intensity level and \( $n_k$ \) is the number of pixels with intensity \( $r_k$ \).

2. **Cumulative Distribution Function (CDF)**:
   \[
   $cdf(r_k) = \sum_{j=0}^{k} p(r_j)$
   \]
   where \( $p(r_j)$ \) is the probability of intensity \($r_j$ \).

3. **Mapping Function**:
   \[
   $s = G^{-1}(cdf_{input}(r))$
   \]
   where \( $G^{-1}$ \) is the inverse CDF of the reference image.

## Example

Let's consider an example where we have an input image and a reference image. The goal is to transform the input image so that its histogram matches that of the reference image.

### Python Implementation

Here's a simple implementation in Python:

```python
import cv2
import numpy as np
from matplotlib import pyplot as plt

def calculate_cdf(hist):
    cdf = hist.cumsum()
    cdf_normalized = cdf / cdf.max()
    return cdf_normalized

# Load the images
input_img = cv2.imread('input_image.jpg', 0)
reference_img = cv2.imread('reference_image.jpg', 0)

# Calculate histograms
input_hist = cv2.calcHist([input_img], [0], None, [256], [0, 256])
reference_hist = cv2.calcHist([reference_img], [0], None, [256], [0, 256])

# Calculate CDFs
input_cdf = calculate_cdf(input_hist)
reference_cdf = calculate_cdf(reference_hist)

# Create a mapping function
mapping = np.zeros(256)
for i in range(256):
    diff = np.abs(reference_cdf - input_cdf[i])
    mapping[i] = np.argmin(diff)

# Apply the mapping to the input image
matched_img = cv2.LUT(input_img, mapping.astype(np.uint8))

# Display the results
plt.subplot(131), plt.imshow(input_img, cmap='gray'), plt.title('Input Image')
plt.subplot(132), plt.imshow(reference_img, cmap='gray'), plt.title('Reference Image')
plt.subplot(133), plt.imshow(matched_img, cmap='gray'), plt.title('Matched Image')
plt.show()
