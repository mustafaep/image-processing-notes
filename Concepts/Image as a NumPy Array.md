---
tags: [concept, image-basics]
week: 1
section: "02 - NumPy and Image Basics"
---

# Image as a NumPy Array

## Definition (in my own words)
A digital image is a grid of pixels, and every pixel is a number (grayscale) or a small group of numbers (color). In Python this grid is a [[NumPy Arrays|NumPy array]], so everything we do to images is array math.

## From file to array
```python
from PIL import Image
import numpy as np

pic = Image.open('../DATA/00-puppy.jpg')   # PIL image object, not an array
pic_arr = np.asarray(pic)                  # numpy.ndarray
pic_arr.shape   # (1300, 1950, 3)
pic_arr.dtype   # uint8
```

## Reading the shape
`(1300, 1950, 3)` = **(height, width, channels)**
- 1300 rows → the image is 1300 pixels tall
- 1950 columns → 1950 pixels wide
- 3 channels → Red, Green, Blue (see [[RGB Color Channels]])

Total values: 1300 × 1950 × 3 ≈ 7.6 million numbers.

## Data type: `uint8`
- unsigned 8-bit integer → values **0 to 255**
- 0 = no intensity (black for that channel), 255 = full intensity
- The puppy image actually uses 0–216 (it is a fairly dark photo).

## ⚠️ The array is read-only
```python
pic_arr.flags.writeable   # False
pic_arr[0, 0, 0] = 1      # ValueError: assignment destination is read-only
```
`np.asarray()` shares memory with the PIL image, so NumPy marks it read-only. **Always work on a copy:**
```python
pic_red = pic_arr.copy()
```
This is why both the lecture and the assessment start with `.copy()`.

## Displaying
- `plt.imshow(pic_arr)` → a 3-channel array is shown in true color.
- `plt.imshow(pic_arr[:,:,0])` → a single channel is 2D, so matplotlib applies a **colormap** (default: viridis). Use `cmap='gray'` to see it as intensity. See [[Colormaps]].

## Used in
- Code: `Code/02-02-images-as-numpy-arrays.ipynb`, `Code/02-03-numpy-and-image-assessment.ipynb`
- [[Week 01 - Digital Image Basics]]

## Related
- [[NumPy Arrays]]
- [[RGB Color Channels]]
- [[Colormaps]]
