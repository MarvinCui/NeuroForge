# How To: Apply Mask 3D Accepted

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Check that 3D data is accepted.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `re`
- `warnings`
- `numpy`
- `pytest`
- `nibabel`
- `numpy.testing`
- `sklearn.preprocessing`
- `nilearn._utils`
- `nilearn._utils.testing`
- `nilearn.conftest`
- `nilearn.exceptions`
- `nilearn.image`
- `nilearn.maskers`
- `nilearn.masking`
- `nilearn.surface.surface`

**Setup Required:**
```python
# Fixtures: affine_eye
```

## Step-by-Step Guide

### Step 1: 'Check that 3D data is accepted.'

```python
'Check that 3D data is accepted.'
```

**Verification:**
```python
assert sorted(data_3d.tolist()) == [3.0, 4.0, 12.0]
```

### Step 2: Assign data_3d = Nifti1Image(...)

```python
data_3d = Nifti1Image(np.arange(27, dtype='int32').reshape((3, 3, 3)), affine_eye)
```

### Step 3: Assign mask_data_3d = np.zeros(...)

```python
mask_data_3d = np.zeros((3, 3, 3))
```

### Step 4: Assign unknown = True

```python
mask_data_3d[1, 1, 0] = True
```

### Step 5: Assign unknown = True

```python
mask_data_3d[0, 1, 0] = True
```

### Step 6: Assign unknown = True

```python
mask_data_3d[0, 1, 1] = True
```

### Step 7: Assign data_3d = apply_mask(...)

```python
data_3d = apply_mask(data_3d, Nifti1Image(mask_data_3d, affine_eye))
```

**Verification:**
```python
assert sorted(data_3d.tolist()) == [3.0, 4.0, 12.0]
```


## Complete Example

```python
# Setup
# Fixtures: affine_eye

# Workflow
'Check that 3D data is accepted.'
data_3d = Nifti1Image(np.arange(27, dtype='int32').reshape((3, 3, 3)), affine_eye)
mask_data_3d = np.zeros((3, 3, 3))
mask_data_3d[1, 1, 0] = True
mask_data_3d[0, 1, 0] = True
mask_data_3d[0, 1, 1] = True
data_3d = apply_mask(data_3d, Nifti1Image(mask_data_3d, affine_eye))
assert sorted(data_3d.tolist()) == [3.0, 4.0, 12.0]
```

## Next Steps


---

*Source: test_masking.py:422 | Complexity: Intermediate | Last updated: 2026-05-18*