# How To: Single Transforms

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test single transforms

## Prerequisites

**Required Modules:**
- `pathlib`
- `tempfile`
- `nibabel`
- `numpy`
- `numpy.testing`
- `pytest`
- `dipy.align`
- `dipy.align.imwarp`
- `dipy.core.gradients`
- `dipy.data`
- `dipy.io.gradients`
- `dipy.io.image`
- `dipy.io.stateful_tractogram`
- `dipy.io.streamline`
- `dipy.testing.decorators`
- `dipy.tracking.utils`


## Step-by-Step Guide

### Step 1: Assign moving = subset_b0

```python
moving = subset_b0
```

### Step 2: Assign static = subset_b0

```python
static = subset_b0
```

### Step 3: Assign moving_affine, static_affine = np.eye(...)

```python
moving_affine = static_affine = np.eye(4)
```

### Step 4: Assign reg_methods = value

```python
reg_methods = [center_of_mass, translation, rigid_isoscaling, rigid_scaling, rigid, affine]
```

### Step 5: Assign unknown = func(...)

```python
xformed, affine_mat = func(moving, static, moving_affine=moving_affine, static_affine=static_affine, level_iters=[5, 5], sigmas=[3, 1], factors=[2, 1])
```

### Step 6: Call npt.assert_almost_equal()

```python
npt.assert_almost_equal(affine_mat[:3, :3], np.eye(3), decimal=1)
```


## Complete Example

```python
# Workflow
moving = subset_b0
static = subset_b0
moving_affine = static_affine = np.eye(4)
reg_methods = [center_of_mass, translation, rigid_isoscaling, rigid_scaling, rigid, affine]
for func in reg_methods:
    xformed, affine_mat = func(moving, static, moving_affine=moving_affine, static_affine=static_affine, level_iters=[5, 5], sigmas=[3, 1], factors=[2, 1])
    npt.assert_almost_equal(affine_mat[:3, :3], np.eye(3), decimal=1)
```

## Next Steps


---

*Source: test_api.py:255 | Complexity: Intermediate | Last updated: 2026-05-18*