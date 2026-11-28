---
tags: [concept, numpy]
week: 1
section: "02 - NumPy and Image Basics"
---

# NumPy Arrays

## Definition (in my own words)
A NumPy array (`ndarray`) is a grid of values that all share **one data type**. It can have any number of dimensions: 1D (a vector), 2D (a matrix, like a grayscale image) or 3D (a color image). Math on it is **vectorized**: one line works on every element, with no Python loop.

## How to create one
| Code | Result | Note |
|---|---|---|
| `np.array([1,2,3])` | `array([1, 2, 3])` | from a Python list |
| `np.arange(0, 10, 2)` | `array([0, 2, 4, 6, 8])` | `stop` is **excluded** |
| `np.zeros((10,5))` | 10×5 of `0.` | default dtype is `float64` |
| `np.ones((2,4))` | 2×4 of `1.` | shape = (rows, columns) |
| `np.full((5,5), 10)` | 5×5 of `10` | one call instead of zeros + assignment |
| `np.random.randint(0,100,10)` | 10 random ints | `high` is **excluded** |

`np.random.seed(101)` makes random numbers reproducible. Setting it once and calling `randint` twice gives two **different** arrays, because the generator keeps moving forward.

## Shape: rows first
`shape = (rows, columns)` = `(height, width)`.
This matters later: in images we write `img[y, x]`, **not** `img[x, y]`.

## Useful methods
| Method | Returns | Example (`arr = [95 11 81 70 63 87 75 9 77 40]`) |
|---|---|---|
| `max()` / `min()` | the value | `95` / `9` |
| `argmax()` / `argmin()` | the **index** of that value | `0` / `7` |
| `mean()` | the average | `60.8` |
| `reshape(2,5)` | same data, new shape | element count must stay the same |

## Indexing and slicing
```python
mat = np.arange(0, 100).reshape(10, 10)
mat[0, 1]          # one element -> 1
mat[:, 1]          # column 1 -> shape (10,)
mat[:, 1].reshape(10, 1)   # a real column vector -> shape (10, 1)
mat[2, :]          # row 2
mat[0:3, 0:3] = 0  # top-left 3x3 block -> 0
```

## ⚠️ View vs copy
A slice is a **view** of the same memory, not a new array. Changing a slice changes the original:

```python
mat[0:3, 0:3] = 0      # mat itself is changed
new = mat.copy()       # independent copy
new[0:6, :] = 99       # mat is NOT affected
```
Rule: call `.copy()` before you experiment on data you want to keep. With images this is even more important (see [[Image as a NumPy Array]]).

## Used in
- Code: `Code/02-01-numpy-arrays.ipynb`
- [[Week 01 - Digital Image Basics]]

## Related
- [[Image as a NumPy Array]]
- [[RGB Color Channels]]
