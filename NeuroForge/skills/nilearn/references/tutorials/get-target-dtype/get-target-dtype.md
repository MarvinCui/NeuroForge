# How To: Get Target Dtype

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test get target dtype

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
# Fixtures: affine_eye
```

## Step-by-Step Guide

### Step 1: Assign img = Nifti1Image(...)

```python
img = Nifti1Image(np.ones((2, 2, 2), dtype=np.float64), affine=affine_eye)
```

**Verification:**
```python
assert get_data(img).dtype.kind == 'f'
```

### Step 2: Assign dtype_kind_float = _get_target_dtype(...)

```python
dtype_kind_float = _get_target_dtype(get_data(img).dtype, target_dtype='auto')
```

**Verification:**
```python
assert dtype_kind_float == np.float32
```

### Step 3: Assign hdr = Nifti1Header(...)

```python
hdr = Nifti1Header()
```

**Verification:**
```python
assert get_data(img2).dtype.kind == img2.get_data_dtype().kind == 'i'
```

### Step 4: Call hdr.set_data_dtype()

```python
hdr.set_data_dtype(np.int64)
```

**Verification:**
```python
assert dtype_kind_int == np.int32
```

### Step 5: Assign data = np.ones(...)

```python
data = np.ones((2, 2, 2), dtype=np.int64)
```

### Step 6: Assign img2 = Nifti1Image(...)

```python
img2 = Nifti1Image(data, affine=affine_eye, header=hdr)
```

**Verification:**
```python
assert get_data(img2).dtype.kind == img2.get_data_dtype().kind == 'i'
```

### Step 7: Assign dtype_kind_int = _get_target_dtype(...)

```python
dtype_kind_int = _get_target_dtype(get_data(img2).dtype, target_dtype='auto')
```

**Verification:**
```python
assert dtype_kind_int == np.int32
```


## Complete Example

```python
# Setup
# Fixtures: affine_eye

# Workflow
img = Nifti1Image(np.ones((2, 2, 2), dtype=np.float64), affine=affine_eye)
assert get_data(img).dtype.kind == 'f'
dtype_kind_float = _get_target_dtype(get_data(img).dtype, target_dtype='auto')
assert dtype_kind_float == np.float32
hdr = Nifti1Header()
hdr.set_data_dtype(np.int64)
data = np.ones((2, 2, 2), dtype=np.int64)
img2 = Nifti1Image(data, affine=affine_eye, header=hdr)
assert get_data(img2).dtype.kind == img2.get_data_dtype().kind == 'i'
dtype_kind_int = _get_target_dtype(get_data(img2).dtype, target_dtype='auto')
assert dtype_kind_int == np.int32
```

## Next Steps


---

*Source: test_niimg.py:51 | Complexity: Intermediate | Last updated: 2026-05-18*