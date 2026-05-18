# How To: Roi In Volume

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test roi in volume

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.reconst.utils`


## Step-by-Step Guide

### Step 1: Assign data_shape = value

```python
data_shape = (11, 11, 11, 64)
```

### Step 2: Assign roi_center = np.array(...)

```python
roi_center = np.array([5, 5, 5])
```

### Step 3: Assign roi_radii = np.array(...)

```python
roi_radii = np.array([5, 5, 5])
```

### Step 4: Assign roi_radii_out = _roi_in_volume(...)

```python
roi_radii_out = _roi_in_volume(data_shape, roi_center, roi_radii)
```

### Step 5: Call npt.assert_array_equal()

```python
npt.assert_array_equal(roi_radii_out, np.array([5, 5, 5]))
```

### Step 6: Assign roi_radii = np.array(...)

```python
roi_radii = np.array([6, 6, 6])
```

### Step 7: Assign roi_radii_out = _roi_in_volume(...)

```python
roi_radii_out = _roi_in_volume(data_shape, roi_center, roi_radii)
```

### Step 8: Call npt.assert_array_equal()

```python
npt.assert_array_equal(roi_radii_out, np.array([5, 5, 5]))
```

### Step 9: Assign roi_center = np.array(...)

```python
roi_center = np.array([4, 4, 4])
```

### Step 10: Assign roi_radii = np.array(...)

```python
roi_radii = np.array([5, 5, 5])
```

### Step 11: Assign roi_radii_out = _roi_in_volume(...)

```python
roi_radii_out = _roi_in_volume(data_shape, roi_center, roi_radii)
```

### Step 12: Call npt.assert_array_equal()

```python
npt.assert_array_equal(roi_radii_out, np.array([4, 4, 4]))
```

### Step 13: Assign data_shape = value

```python
data_shape = (11, 11, 1, 64)
```

### Step 14: Assign roi_center = np.array(...)

```python
roi_center = np.array([5, 5, 0])
```

### Step 15: Assign roi_radii = np.array(...)

```python
roi_radii = np.array([5, 5, 0])
```

### Step 16: Assign roi_radii_out = _roi_in_volume(...)

```python
roi_radii_out = _roi_in_volume(data_shape, roi_center, roi_radii)
```

### Step 17: Call npt.assert_array_equal()

```python
npt.assert_array_equal(roi_radii_out, np.array([5, 5, 0]))
```

### Step 18: Assign roi_center = np.array(...)

```python
roi_center = np.array([2, 5, 0])
```

### Step 19: Assign roi_radii = np.array(...)

```python
roi_radii = np.array([5, 10, 2])
```

### Step 20: Assign roi_radii_out = _roi_in_volume(...)

```python
roi_radii_out = _roi_in_volume(data_shape, roi_center, roi_radii)
```

### Step 21: Call npt.assert_array_equal()

```python
npt.assert_array_equal(roi_radii_out, np.array([2, 5, 0]))
```


## Complete Example

```python
# Workflow
data_shape = (11, 11, 11, 64)
roi_center = np.array([5, 5, 5])
roi_radii = np.array([5, 5, 5])
roi_radii_out = _roi_in_volume(data_shape, roi_center, roi_radii)
npt.assert_array_equal(roi_radii_out, np.array([5, 5, 5]))
roi_radii = np.array([6, 6, 6])
roi_radii_out = _roi_in_volume(data_shape, roi_center, roi_radii)
npt.assert_array_equal(roi_radii_out, np.array([5, 5, 5]))
roi_center = np.array([4, 4, 4])
roi_radii = np.array([5, 5, 5])
roi_radii_out = _roi_in_volume(data_shape, roi_center, roi_radii)
npt.assert_array_equal(roi_radii_out, np.array([4, 4, 4]))
data_shape = (11, 11, 1, 64)
roi_center = np.array([5, 5, 0])
roi_radii = np.array([5, 5, 0])
roi_radii_out = _roi_in_volume(data_shape, roi_center, roi_radii)
npt.assert_array_equal(roi_radii_out, np.array([5, 5, 0]))
roi_center = np.array([2, 5, 0])
roi_radii = np.array([5, 10, 2])
roi_radii_out = _roi_in_volume(data_shape, roi_center, roi_radii)
npt.assert_array_equal(roi_radii_out, np.array([2, 5, 0]))
```

## Next Steps


---

*Source: test_utils.py:7 | Complexity: Advanced | Last updated: 2026-05-18*