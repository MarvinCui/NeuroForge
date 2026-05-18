# How To: Mask

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test mask

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `pytest`
- `scipy.ndimage`
- `dipy.data`
- `dipy.io.image`
- `dipy.segment.mask`
- `dipy.utils.deprecator`


## Step-by-Step Guide

### Step 1: Assign vol = np.zeros(...)

```python
vol = np.zeros((30, 30, 30))
```

**Verification:**
```python
assert_equal(initial_otsu, initial)
```

### Step 2: Assign unknown = 1

```python
vol[15, 15, 15] = 1
```

**Verification:**
```python
assert_equal(initial_crop, initial)
```

### Step 3: Assign struct = generate_binary_structure(...)

```python
struct = generate_binary_structure(3, 1)
```

**Verification:**
```python
assert_equal(final, initial)
```

### Step 4: Assign voln = binary_dilation.astype(...)

```python
voln = binary_dilation(vol, structure=struct, iterations=4).astype('f4')
```

**Verification:**
```python
assert_equal(img, img_copy)
```

### Step 5: Assign initial = np.sum(...)

```python
initial = np.sum(voln > 0)
```

**Verification:**
```python
assert_equal(median_test, median_control)
```

### Step 6: Assign mask = voln.copy(...)

```python
mask = voln.copy()
```

### Step 7: Assign thresh = otsu(...)

```python
thresh = otsu(mask)
```

### Step 8: Assign mask = value

```python
mask = mask > thresh
```

### Step 9: Assign initial_otsu = np.sum(...)

```python
initial_otsu = np.sum(mask > 0)
```

### Step 10: Call assert_equal()

```python
assert_equal(initial_otsu, initial)
```

### Step 11: Assign unknown = bounding_box(...)

```python
mins, maxs = bounding_box(mask)
```

### Step 12: Assign voln_crop = crop(...)

```python
voln_crop = crop(mask, mins, maxs)
```

### Step 13: Assign initial_crop = np.sum(...)

```python
initial_crop = np.sum(voln_crop > 0)
```

### Step 14: Call assert_equal()

```python
assert_equal(initial_crop, initial)
```

### Step 15: Call applymask()

```python
applymask(voln, mask)
```

### Step 16: Assign final = np.sum(...)

```python
final = np.sum(voln > 0)
```

### Step 17: Call assert_equal()

```python
assert_equal(final, initial)
```

### Step 18: Assign img = np.arange.reshape(...)

```python
img = np.arange(25).reshape(5, 5)
```

### Step 19: Assign img_copy = img.copy(...)

```python
img_copy = img.copy()
```

### Step 20: Assign medianradius = 2

```python
medianradius = 2
```

### Step 21: Assign median_test = multi_median(...)

```python
median_test = multi_median(img, medianradius, 3)
```

### Step 22: Call assert_equal()

```python
assert_equal(img, img_copy)
```

### Step 23: Assign medarr = value

```python
medarr = np.ones_like(img.shape) * (medianradius * 2 + 1)
```

### Step 24: Assign median_control = median_filter(...)

```python
median_control = median_filter(img, medarr)
```

### Step 25: Assign median_control = median_filter(...)

```python
median_control = median_filter(median_control, medarr)
```

### Step 26: Assign median_control = median_filter(...)

```python
median_control = median_filter(median_control, medarr)
```

### Step 27: Call assert_equal()

```python
assert_equal(median_test, median_control)
```


## Complete Example

```python
# Workflow
vol = np.zeros((30, 30, 30))
vol[15, 15, 15] = 1
struct = generate_binary_structure(3, 1)
voln = binary_dilation(vol, structure=struct, iterations=4).astype('f4')
initial = np.sum(voln > 0)
mask = voln.copy()
thresh = otsu(mask)
mask = mask > thresh
initial_otsu = np.sum(mask > 0)
assert_equal(initial_otsu, initial)
mins, maxs = bounding_box(mask)
voln_crop = crop(mask, mins, maxs)
initial_crop = np.sum(voln_crop > 0)
assert_equal(initial_crop, initial)
applymask(voln, mask)
final = np.sum(voln > 0)
assert_equal(final, initial)
img = np.arange(25).reshape(5, 5)
img_copy = img.copy()
medianradius = 2
median_test = multi_median(img, medianradius, 3)
assert_equal(img, img_copy)
medarr = np.ones_like(img.shape) * (medianradius * 2 + 1)
median_control = median_filter(img, medarr)
median_control = median_filter(median_control, medarr)
median_control = median_filter(median_control, medarr)
assert_equal(median_test, median_control)
```

## Next Steps


---

*Source: test_mask.py:21 | Complexity: Advanced | Last updated: 2026-05-18*