# How To: Rigid Scaling

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test rigid scaling

## Prerequisites

**Required Modules:**
- `logging`
- `pathlib`
- `tempfile`
- `nibabel`
- `numpy`
- `numpy.testing`
- `pytest`
- `dipy.align.tests.test_imwarp`
- `dipy.align.tests.test_parzenhist`
- `dipy.align.transforms`
- `dipy.data`
- `dipy.io.image`
- `dipy.io.stateful_tractogram`
- `dipy.io.streamline`
- `dipy.testing.decorators`
- `dipy.tracking.streamline`
- `dipy.utils.optpkg`
- `dipy.workflows.align`
- `logging`


## Step-by-Step Guide

### Step 1: Assign out_moved = value

```python
out_moved = Path(temp_out_dir) / 'rigid_scaling_moved.nii.gz'
```

### Step 2: Assign out_affine = value

```python
out_affine = Path(temp_out_dir) / 'rigid_scaling_affine.txt'
```

### Step 3: Assign image_registration_flow._force_overwrite = True

```python
image_registration_flow._force_overwrite = True
```

### Step 4: Call image_registration_flow.run()

```python
image_registration_flow.run(static_image_file, moving_image_file, transform='rigid_scaling', out_dir=temp_out_dir, out_moved=out_moved, out_affine=out_affine, save_metric=True, level_iters=[100, 10, 1], out_quality='rigid_scaling_q.txt')
```

### Step 5: Assign dist = read_distance(...)

```python
dist = read_distance('rigid_scaling_q.txt')
```

### Step 6: Call npt.assert_almost_equal()

```python
npt.assert_almost_equal(dist, -0.698688892993124, 1)
```

### Step 7: Call check_existence()

```python
check_existence(out_moved, out_affine)
```


## Complete Example

```python
# Workflow
out_moved = Path(temp_out_dir) / 'rigid_scaling_moved.nii.gz'
out_affine = Path(temp_out_dir) / 'rigid_scaling_affine.txt'
image_registration_flow._force_overwrite = True
image_registration_flow.run(static_image_file, moving_image_file, transform='rigid_scaling', out_dir=temp_out_dir, out_moved=out_moved, out_affine=out_affine, save_metric=True, level_iters=[100, 10, 1], out_quality='rigid_scaling_q.txt')
dist = read_distance('rigid_scaling_q.txt')
npt.assert_almost_equal(dist, -0.698688892993124, 1)
check_existence(out_moved, out_affine)
```

## Next Steps


---

*Source: test_align.py:410 | Complexity: Intermediate | Last updated: 2026-05-18*