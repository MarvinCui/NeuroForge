# How To: Mask From Roi

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test mask from roi

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.reconst.utils`


## Step-by-Step Guide

### Step 1: Assign data_shape = value

```python
data_shape = (5, 5, 5)
```

### Step 2: Assign roi_center = value

```python
roi_center = (2, 2, 2)
```

### Step 3: Assign roi_radii = value

```python
roi_radii = (2, 2, 2)
```

### Step 4: Assign mask_gt = np.ones(...)

```python
mask_gt = np.ones(data_shape)
```

### Step 5: Assign roi_mask = _mask_from_roi(...)

```python
roi_mask = _mask_from_roi(data_shape, roi_center, roi_radii)
```

### Step 6: Call npt.assert_array_equal()

```python
npt.assert_array_equal(roi_mask, mask_gt)
```

### Step 7: Assign roi_radii = value

```python
roi_radii = (1, 2, 2)
```

### Step 8: Assign mask_gt = np.zeros(...)

```python
mask_gt = np.zeros(data_shape)
```

### Step 9: Assign unknown = 1

```python
mask_gt[1:4, 0:5, 0:5] = 1
```

### Step 10: Assign roi_mask = _mask_from_roi(...)

```python
roi_mask = _mask_from_roi(data_shape, roi_center, roi_radii)
```

### Step 11: Call npt.assert_array_equal()

```python
npt.assert_array_equal(roi_mask, mask_gt)
```

### Step 12: Assign roi_radii = value

```python
roi_radii = (0, 2, 2)
```

### Step 13: Assign mask_gt = np.zeros(...)

```python
mask_gt = np.zeros(data_shape)
```

### Step 14: Assign unknown = 1

```python
mask_gt[2, 0:5, 0:5] = 1
```

### Step 15: Assign roi_mask = _mask_from_roi(...)

```python
roi_mask = _mask_from_roi(data_shape, roi_center, roi_radii)
```

### Step 16: Call npt.assert_array_equal()

```python
npt.assert_array_equal(roi_mask, mask_gt)
```


## Complete Example

```python
# Workflow
data_shape = (5, 5, 5)
roi_center = (2, 2, 2)
roi_radii = (2, 2, 2)
mask_gt = np.ones(data_shape)
roi_mask = _mask_from_roi(data_shape, roi_center, roi_radii)
npt.assert_array_equal(roi_mask, mask_gt)
roi_radii = (1, 2, 2)
mask_gt = np.zeros(data_shape)
mask_gt[1:4, 0:5, 0:5] = 1
roi_mask = _mask_from_roi(data_shape, roi_center, roi_radii)
npt.assert_array_equal(roi_mask, mask_gt)
roi_radii = (0, 2, 2)
mask_gt = np.zeros(data_shape)
mask_gt[2, 0:5, 0:5] = 1
roi_mask = _mask_from_roi(data_shape, roi_center, roi_radii)
npt.assert_array_equal(roi_mask, mask_gt)
```

## Next Steps


---

*Source: test_utils.py:35 | Complexity: Advanced | Last updated: 2026-05-18*