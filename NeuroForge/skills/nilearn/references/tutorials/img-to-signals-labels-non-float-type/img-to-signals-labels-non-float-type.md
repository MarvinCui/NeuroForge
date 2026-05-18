# How To: Img To Signals Labels Non Float Type

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test img to signals labels non float type

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `warnings`
- `numpy`
- `pytest`
- `nibabel`
- `numpy.testing`
- `nilearn._utils.data_gen`
- `nilearn._utils.testing`
- `nilearn.conftest`
- `nilearn.exceptions`
- `nilearn.image`
- `nilearn.maskers`
- `nilearn.regions.signal_extraction`

**Setup Required:**
```python
# Fixtures: target_dtype, rng
```

## Step-by-Step Guide

### Step 1: Assign fake_fmri_data = value

```python
fake_fmri_data = rng.uniform(size=(10, 10, 10, N_TIMEPOINTS)) > 0.5
```

**Verification:**
```python
assert np.sum(timeseries_int) != 0
```

### Step 2: Assign fake_affine = np.eye.astype(...)

```python
fake_affine = np.eye(4, 4).astype(np.float64)
```

**Verification:**
```python
assert np.allclose(timeseries_int, timeseries_float)
```

### Step 3: Assign fake_fmri_img_orig = Nifti1Image(...)

```python
fake_fmri_img_orig = Nifti1Image(fake_fmri_data.astype(np.float64), fake_affine)
```

### Step 4: Assign fake_fmri_img_target_dtype = new_img_like(...)

```python
fake_fmri_img_target_dtype = new_img_like(fake_fmri_img_orig, fake_fmri_data.astype(target_dtype))
```

### Step 5: Assign fake_mask_data = np.zeros(...)

```python
fake_mask_data = np.zeros((10, 10, 10), dtype=np.uint8)
```

### Step 6: Assign unknown = 1

```python
fake_mask_data[1:8, 1:8, 1:8] = 1
```

### Step 7: Assign fake_mask = Nifti1Image(...)

```python
fake_mask = Nifti1Image(fake_mask_data, fake_affine)
```

### Step 8: Assign masker = NiftiLabelsMasker(...)

```python
masker = NiftiLabelsMasker(fake_mask, standardize=None)
```

### Step 9: Call masker.fit()

```python
masker.fit()
```

### Step 10: Assign timeseries_int = masker.transform(...)

```python
timeseries_int = masker.transform(fake_fmri_img_target_dtype)
```

### Step 11: Assign timeseries_float = masker.transform(...)

```python
timeseries_float = masker.transform(fake_fmri_img_orig)
```

**Verification:**
```python
assert np.sum(timeseries_int) != 0
```


## Complete Example

```python
# Setup
# Fixtures: target_dtype, rng

# Workflow
fake_fmri_data = rng.uniform(size=(10, 10, 10, N_TIMEPOINTS)) > 0.5
fake_affine = np.eye(4, 4).astype(np.float64)
fake_fmri_img_orig = Nifti1Image(fake_fmri_data.astype(np.float64), fake_affine)
fake_fmri_img_target_dtype = new_img_like(fake_fmri_img_orig, fake_fmri_data.astype(target_dtype))
fake_mask_data = np.zeros((10, 10, 10), dtype=np.uint8)
fake_mask_data[1:8, 1:8, 1:8] = 1
fake_mask = Nifti1Image(fake_mask_data, fake_affine)
masker = NiftiLabelsMasker(fake_mask, standardize=None)
masker.fit()
timeseries_int = masker.transform(fake_fmri_img_target_dtype)
timeseries_float = masker.transform(fake_fmri_img_orig)
assert np.sum(timeseries_int) != 0
assert np.allclose(timeseries_int, timeseries_float)
```

## Next Steps


---

*Source: test_signal_extraction.py:808 | Complexity: Advanced | Last updated: 2026-05-18*