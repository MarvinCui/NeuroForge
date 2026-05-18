# How To: 4D Moving

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test 4D moving

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
out_moved = Path(temp_out_dir) / 'trans_moved.nii.gz'
```

**Verification:**
```python
assert volume.ndim == 4
```

### Step 2: Assign out_affine = value

```python
out_affine = Path(temp_out_dir) / 'trans_affine.txt'
```

### Step 3: Assign image_registration_flow._force_overwrite = True

```python
image_registration_flow._force_overwrite = True
```

### Step 4: Assign kwargs = value

```python
kwargs = {'static_image_files': static_image_file, 'moving_image_files': dwi_image_file, 'transform': 'trans', 'out_dir': temp_out_dir, 'out_moved': out_moved, 'out_affine': out_affine, 'save_metric': True, 'level_iters': [100, 10, 1], 'out_quality': 'trans_q.txt'}
```

### Step 5: Call image_registration_flow.run()

```python
image_registration_flow.run(moving_vol_idx=0, **kwargs)
```

### Step 6: Assign dist = read_distance(...)

```python
dist = read_distance('trans_q.txt')
```

### Step 7: Call npt.assert_almost_equal()

```python
npt.assert_almost_equal(float(dist), -1.0002607616786339, 1)
```

### Step 8: Call check_existence()

```python
check_existence(out_moved, out_affine)
```

### Step 9: Call apply_trans.run()

```python
apply_trans.run(static_image_files=static_image_file, moving_image_files=dwi_image_file, out_dir=temp_out_dir, transform_map_file=out_affine, out_file='transformed2.nii.gz')
```

### Step 10: Assign volume = load_nifti_data(...)

```python
volume = load_nifti_data(Path(temp_out_dir) / 'transformed2.nii.gz')
```

**Verification:**
```python
assert volume.ndim == 4
```

### Step 11: Call image_registration_flow.run()

```python
image_registration_flow.run(**kwargs)
```


## Complete Example

```python
# Workflow
out_moved = Path(temp_out_dir) / 'trans_moved.nii.gz'
out_affine = Path(temp_out_dir) / 'trans_affine.txt'
image_registration_flow._force_overwrite = True
kwargs = {'static_image_files': static_image_file, 'moving_image_files': dwi_image_file, 'transform': 'trans', 'out_dir': temp_out_dir, 'out_moved': out_moved, 'out_affine': out_affine, 'save_metric': True, 'level_iters': [100, 10, 1], 'out_quality': 'trans_q.txt'}
with pytest.raises(ValueError, match='Dimension mismatch'):
    image_registration_flow.run(**kwargs)
image_registration_flow.run(moving_vol_idx=0, **kwargs)
dist = read_distance('trans_q.txt')
npt.assert_almost_equal(float(dist), -1.0002607616786339, 1)
check_existence(out_moved, out_affine)
apply_trans.run(static_image_files=static_image_file, moving_image_files=dwi_image_file, out_dir=temp_out_dir, transform_map_file=out_affine, out_file='transformed2.nii.gz')
volume = load_nifti_data(Path(temp_out_dir) / 'transformed2.nii.gz')
assert volume.ndim == 4
```

## Next Steps


---

*Source: test_align.py:513 | Complexity: Advanced | Last updated: 2026-05-18*