# How To: Voxel2Streamline

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test voxel2streamline

## Prerequisites

**Required Modules:**
- `os.path`
- `nibabel`
- `numpy`
- `numpy.testing`
- `scipy.linalg`
- `dipy.core.gradients`
- `dipy.core.optimize`
- `dipy.data`
- `dipy.io.gradients`
- `dipy.io.image`
- `dipy.io.stateful_tractogram`
- `dipy.tracking.life`


## Step-by-Step Guide

### Step 1: Assign streamline = value

```python
streamline = [[[1.1, 2.4, 2.9], [4, 5, 3], [5, 6, 3], [6, 7, 3]], [[1, 2, 3], [4, 5, 3], [5, 6, 3]]]
```

### Step 2: Assign affine = np.eye(...)

```python
affine = np.eye(4)
```

### Step 3: Assign unknown = life.voxel2streamline(...)

```python
v2f, v2fn = life.voxel2streamline(streamline, affine)
```

### Step 4: Call npt.assert_equal()

```python
npt.assert_equal(v2f, {0: [0, 1], 1: [0, 1], 2: [0, 1], 3: [0]})
```

### Step 5: Call npt.assert_equal()

```python
npt.assert_equal(v2fn, {0: {0: [0], 1: [1], 2: [2], 3: [3]}, 1: {0: [0], 1: [1], 2: [2]}})
```

### Step 6: Assign affine = np.array(...)

```python
affine = np.array([[0.9, 0, 0, 10], [0, 0.9, 0, -100], [0, 0, 0.9, 2], [0, 0, 0, 1]])
```

### Step 7: Assign xform_sl = life.transform_streamlines(...)

```python
xform_sl = life.transform_streamlines(streamline, np.linalg.inv(affine))
```

### Step 8: Assign unknown = life.voxel2streamline(...)

```python
v2f, v2fn = life.voxel2streamline(xform_sl, affine)
```

### Step 9: Call npt.assert_equal()

```python
npt.assert_equal(v2f, {0: [0, 1], 1: [0, 1], 2: [0, 1], 3: [0]})
```

### Step 10: Call npt.assert_equal()

```python
npt.assert_equal(v2fn, {0: {0: [0], 1: [1], 2: [2], 3: [3]}, 1: {0: [0], 1: [1], 2: [2]}})
```


## Complete Example

```python
# Workflow
streamline = [[[1.1, 2.4, 2.9], [4, 5, 3], [5, 6, 3], [6, 7, 3]], [[1, 2, 3], [4, 5, 3], [5, 6, 3]]]
affine = np.eye(4)
v2f, v2fn = life.voxel2streamline(streamline, affine)
npt.assert_equal(v2f, {0: [0, 1], 1: [0, 1], 2: [0, 1], 3: [0]})
npt.assert_equal(v2fn, {0: {0: [0], 1: [1], 2: [2], 3: [3]}, 1: {0: [0], 1: [1], 2: [2]}})
affine = np.array([[0.9, 0, 0, 10], [0, 0.9, 0, -100], [0, 0, 0.9, 2], [0, 0, 0, 1]])
xform_sl = life.transform_streamlines(streamline, np.linalg.inv(affine))
v2f, v2fn = life.voxel2streamline(xform_sl, affine)
npt.assert_equal(v2f, {0: [0, 1], 1: [0, 1], 2: [0, 1], 3: [0]})
npt.assert_equal(v2fn, {0: {0: [0], 1: [1], 2: [2], 3: [3]}, 1: {0: [0], 1: [1], 2: [2]}})
```

## Next Steps


---

*Source: test_life.py:75 | Complexity: Advanced | Last updated: 2026-05-18*