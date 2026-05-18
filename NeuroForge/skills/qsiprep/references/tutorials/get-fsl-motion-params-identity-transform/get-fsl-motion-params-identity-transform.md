# How To: Get Fsl Motion Params Identity Transform

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test end-to-end motion parameter extraction using c3d_affine_tool.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `shutil`
- `nibabel`
- `numpy`
- `pytest`
- `SimpleITK`
- `qsiprep.interfaces.gradients`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test end-to-end motion parameter extraction using c3d_affine_tool.'

```python
'Test end-to-end motion parameter extraction using c3d_affine_tool.'
```

**Verification:**
```python
assert motion_params.shape == (12,)
```

### Step 2: Assign ref_file = os.path.join(...)

```python
ref_file = os.path.join(tmp_path, 'ref.nii.gz')
```

### Step 3: Assign itk_file = os.path.join(...)

```python
itk_file = os.path.join(tmp_path, 'transform0GenericAffine.mat')
```

### Step 4: Assign ref_img = nb.Nifti1Image(...)

```python
ref_img = nb.Nifti1Image(np.zeros((5, 5, 5), dtype=np.float32), affine=np.eye(4))
```

### Step 5: Call ref_img.to_filename()

```python
ref_img.to_filename(ref_file)
```

### Step 6: Call sitk.WriteTransform()

```python
sitk.WriteTransform(sitk.AffineTransform(3), itk_file)
```

### Step 7: Assign motion_params = get_fsl_motion_params(...)

```python
motion_params = get_fsl_motion_params(itk_file, ref_file, str(tmp_path))
```

**Verification:**
```python
assert motion_params.shape == (12,)
```

### Step 8: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(motion_params[:3], [1.0, 1.0, 1.0], atol=1e-08)
```

### Step 9: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(motion_params[3:], np.zeros(9), atol=1e-08)
```

### Step 10: Call pytest.skip()

```python
pytest.skip('c3d_affine_tool is required for this test')
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test end-to-end motion parameter extraction using c3d_affine_tool.'
if shutil.which('c3d_affine_tool') is None:
    pytest.skip('c3d_affine_tool is required for this test')
ref_file = os.path.join(tmp_path, 'ref.nii.gz')
itk_file = os.path.join(tmp_path, 'transform0GenericAffine.mat')
ref_img = nb.Nifti1Image(np.zeros((5, 5, 5), dtype=np.float32), affine=np.eye(4))
ref_img.to_filename(ref_file)
sitk.WriteTransform(sitk.AffineTransform(3), itk_file)
motion_params = get_fsl_motion_params(itk_file, ref_file, str(tmp_path))
assert motion_params.shape == (12,)
np.testing.assert_allclose(motion_params[:3], [1.0, 1.0, 1.0], atol=1e-08)
np.testing.assert_allclose(motion_params[3:], np.zeros(9), atol=1e-08)
```

## Next Steps


---

*Source: test_interfaces_gradients.py:14 | Complexity: Advanced | Last updated: 2026-05-18*