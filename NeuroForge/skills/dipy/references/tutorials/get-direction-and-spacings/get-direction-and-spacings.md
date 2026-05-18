# How To: Get Direction And Spacings

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test direction and spacings from affine transforms

## Prerequisites

**Required Modules:**
- `nibabel.eulerangles`
- `numpy`
- `numpy.testing`
- `dipy.align`
- `dipy.align.imwarp`
- `dipy.core.interpolation`
- `dipy.data`
- `dipy.testing.decorators`
- `dipy.tracking.streamline`


## Step-by-Step Guide

### Step 1: 'Test direction and spacings from affine transforms'

```python
'Test direction and spacings from affine transforms'
```

**Verification:**
```python
assert_array_almost_equal(direction, direction_gt)
```

### Step 2: Assign xrot = 0.5

```python
xrot = 0.5
```

**Verification:**
```python
assert_array_almost_equal(spacings, spacings_gt)
```

### Step 3: Assign yrot = 0.75

```python
yrot = 0.75
```

### Step 4: Assign zrot = 1.0

```python
zrot = 1.0
```

### Step 5: Assign direction_gt = eulerangles.euler2mat(...)

```python
direction_gt = eulerangles.euler2mat(zrot, yrot, xrot)
```

### Step 6: Assign spacings_gt = np.array(...)

```python
spacings_gt = np.array([1.1, 1.2, 1.3])
```

### Step 7: Assign scaling_gt = np.diag(...)

```python
scaling_gt = np.diag(spacings_gt)
```

### Step 8: Assign translation_gt = np.array(...)

```python
translation_gt = np.array([1, 2, 3])
```

### Step 9: Assign affine = np.eye(...)

```python
affine = np.eye(4)
```

### Step 10: Assign unknown = direction_gt.dot(...)

```python
affine[:3, :3] = direction_gt.dot(scaling_gt)
```

### Step 11: Assign unknown = translation_gt

```python
affine[:3, 3] = translation_gt
```

### Step 12: Assign unknown = imwarp.get_direction_and_spacings(...)

```python
direction, spacings = imwarp.get_direction_and_spacings(affine, 3)
```

### Step 13: Call assert_array_almost_equal()

```python
assert_array_almost_equal(direction, direction_gt)
```

### Step 14: Call assert_array_almost_equal()

```python
assert_array_almost_equal(spacings, spacings_gt)
```


## Complete Example

```python
# Workflow
'Test direction and spacings from affine transforms'
xrot = 0.5
yrot = 0.75
zrot = 1.0
direction_gt = eulerangles.euler2mat(zrot, yrot, xrot)
spacings_gt = np.array([1.1, 1.2, 1.3])
scaling_gt = np.diag(spacings_gt)
translation_gt = np.array([1, 2, 3])
affine = np.eye(4)
affine[:3, :3] = direction_gt.dot(scaling_gt)
affine[:3, 3] = translation_gt
direction, spacings = imwarp.get_direction_and_spacings(affine, 3)
assert_array_almost_equal(direction, direction_gt)
assert_array_almost_equal(spacings, spacings_gt)
```

## Next Steps


---

*Source: test_imwarp.py:378 | Complexity: Advanced | Last updated: 2026-05-18*