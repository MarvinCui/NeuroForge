# How To: Img Data Dtype

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test img data dtype

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `warnings`
- `pathlib`
- `tempfile`
- `joblib`
- `numpy`
- `pytest`
- `nibabel`
- `nilearn._utils.niimg`
- `nilearn._utils.testing`
- `nilearn.image`

**Setup Required:**
```python
# Fixtures: rng, affine_eye, tmp_path
```

## Step-by-Step Guide

### Step 1: Assign nifti1_dtypes = value

```python
nifti1_dtypes = (np.uint8, np.uint16, np.uint32, np.uint64, np.int8, np.int16, np.int32, np.float32, np.float64)
```

**Verification:**
```python
assert np.array(loaded.dataobj).dtype == img_data_dtype(loaded)
```

### Step 2: Assign dtype_matches = value

```python
dtype_matches = []
```

**Verification:**
```python
assert any(dtype_matches)
```

### Step 3: Assign hdr = Nifti1Header(...)

```python
hdr = Nifti1Header()
```

**Verification:**
```python
assert not all(dtype_matches)
```

### Step 4: Assign dataobj = rng.uniform.astype(...)

```python
dataobj = rng.uniform(0, 255, (2, 2, 2)).astype(logical_dtype)
```

### Step 5: Call hdr.set_data_dtype()

```python
hdr.set_data_dtype(on_disk_dtype)
```

### Step 6: Assign img = Nifti1Image(...)

```python
img = Nifti1Image(dataobj, affine_eye, header=hdr)
```

### Step 7: Call img.to_filename()

```python
img.to_filename(tmp_path / 'test.nii')
```

### Step 8: Assign loaded = load(...)

```python
loaded = load(tmp_path / 'test.nii')
```

### Step 9: Call dtype_matches.append()

```python
dtype_matches.append(loaded.get_data_dtype() == img_data_dtype(loaded))
```

### Step 10: Call warnings.simplefilter()

```python
warnings.simplefilter('ignore', category=DeprecationWarning)
```

**Verification:**
```python
assert np.array(loaded.dataobj).dtype == img_data_dtype(loaded)
```


## Complete Example

```python
# Setup
# Fixtures: rng, affine_eye, tmp_path

# Workflow
nifti1_dtypes = (np.uint8, np.uint16, np.uint32, np.uint64, np.int8, np.int16, np.int32, np.float32, np.float64)
dtype_matches = []
hdr = Nifti1Header()
for logical_dtype in nifti1_dtypes:
    dataobj = rng.uniform(0, 255, (2, 2, 2)).astype(logical_dtype)
    for on_disk_dtype in nifti1_dtypes:
        hdr.set_data_dtype(on_disk_dtype)
        img = Nifti1Image(dataobj, affine_eye, header=hdr)
        img.to_filename(tmp_path / 'test.nii')
        loaded = load(tmp_path / 'test.nii')
        dtype_matches.append(loaded.get_data_dtype() == img_data_dtype(loaded))
        with warnings.catch_warnings():
            warnings.simplefilter('ignore', category=DeprecationWarning)
            assert np.array(loaded.dataobj).dtype == img_data_dtype(loaded)
assert any(dtype_matches)
assert not all(dtype_matches)
```

## Next Steps


---

*Source: test_niimg.py:71 | Complexity: Advanced | Last updated: 2026-05-18*