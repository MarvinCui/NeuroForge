# How To: Fibermodel Init

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test FiberModel init

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

### Step 1: Assign unknown = dpd.get_fnames(...)

```python
data_file, bval_file, bvec_file = dpd.get_fnames(name='small_64D')
```

### Step 2: Assign unknown = read_bvals_bvecs(...)

```python
bvals, bvecs = read_bvals_bvecs(bval_file, bvec_file)
```

### Step 3: Assign gtab = grad.gradient_table(...)

```python
gtab = grad.gradient_table(bvals, bvecs=bvecs)
```

### Step 4: Assign FM = life.FiberModel(...)

```python
FM = life.FiberModel(gtab)
```

### Step 5: Assign streamline_cases = value

```python
streamline_cases = [[[[1, 2, 3], [4, 5, 3], [5, 6, 3], [6, 7, 3]], [[1, 2, 3], [4, 5, 3], [5, 6, 3]]], [[[1, 2, 3]], [[1, 2, 3], [4, 5, 3], [5, 6, 3]]]]
```

### Step 6: Assign affine = np.eye(...)

```python
affine = np.eye(4)
```

### Step 7: Assign unknown = FM.setup(...)

```python
fiber_matrix, vox_coords = FM.setup(streamline_cases[0], affine, sphere=sphere)
```

### Step 8: Call npt.assert_array_equal()

```python
npt.assert_array_equal(np.array(vox_coords), np.array([[1, 2, 3], [4, 5, 3], [5, 6, 3], [6, 7, 3]]))
```

### Step 9: Call npt.assert_equal()

```python
npt.assert_equal(fiber_matrix.shape, (len(vox_coords) * 64, len(streamline_cases[0])))
```

### Step 10: Call npt.assert_raises()

```python
npt.assert_raises(IndexError, FM.setup, streamline_cases[1], affine, sphere=sphere)
```


## Complete Example

```python
# Workflow
data_file, bval_file, bvec_file = dpd.get_fnames(name='small_64D')
bvals, bvecs = read_bvals_bvecs(bval_file, bvec_file)
gtab = grad.gradient_table(bvals, bvecs=bvecs)
FM = life.FiberModel(gtab)
streamline_cases = [[[[1, 2, 3], [4, 5, 3], [5, 6, 3], [6, 7, 3]], [[1, 2, 3], [4, 5, 3], [5, 6, 3]]], [[[1, 2, 3]], [[1, 2, 3], [4, 5, 3], [5, 6, 3]]]]
affine = np.eye(4)
for sphere in [None, False, dpd.get_sphere(name='symmetric362')]:
    fiber_matrix, vox_coords = FM.setup(streamline_cases[0], affine, sphere=sphere)
    npt.assert_array_equal(np.array(vox_coords), np.array([[1, 2, 3], [4, 5, 3], [5, 6, 3], [6, 7, 3]]))
    npt.assert_equal(fiber_matrix.shape, (len(vox_coords) * 64, len(streamline_cases[0])))
    npt.assert_raises(IndexError, FM.setup, streamline_cases[1], affine, sphere=sphere)
```

## Next Steps


---

*Source: test_life.py:98 | Complexity: Advanced | Last updated: 2026-05-18*