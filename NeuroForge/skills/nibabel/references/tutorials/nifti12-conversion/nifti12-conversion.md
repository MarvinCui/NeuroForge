# How To: Nifti12 Conversion

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test nifti12 conversion

## Prerequisites

**Required Modules:**
- `os`
- `numpy`
- `pytest`
- `numpy.testing`
- `nifti1`
- `nifti2`
- `testing`


## Step-by-Step Guide

### Step 1: Assign shape = value

```python
shape = (2, 3, 4)
```

**Verification:**
```python
assert out_hdr.get_data_shape() == shape
```

### Step 2: Assign dtype_type = value

```python
dtype_type = np.int64
```

**Verification:**
```python
assert out_hdr.get_data_dtype() == dtype_type
```

### Step 3: Assign ext1 = Nifti1Extension(...)

```python
ext1 = Nifti1Extension(6, b'My comment')
```

**Verification:**
```python
assert in_hdr.extensions == out_hdr.extensions
```

### Step 4: Assign ext2 = Nifti1Extension(...)

```python
ext2 = Nifti1Extension(6, b'Fresh comment')
```

### Step 5: Assign in_hdr = in_type(...)

```python
in_hdr = in_type()
```

### Step 6: Call in_hdr.set_data_shape()

```python
in_hdr.set_data_shape(shape)
```

### Step 7: Call in_hdr.set_data_dtype()

```python
in_hdr.set_data_dtype(dtype_type)
```

### Step 8: Assign unknown = value

```python
in_hdr.extensions[:] = [ext1, ext2]
```

### Step 9: Assign out_hdr = out_type.from_header(...)

```python
out_hdr = out_type.from_header(in_hdr)
```

**Verification:**
```python
assert out_hdr.get_data_shape() == shape
```


## Complete Example

```python
# Workflow
shape = (2, 3, 4)
dtype_type = np.int64
ext1 = Nifti1Extension(6, b'My comment')
ext2 = Nifti1Extension(6, b'Fresh comment')
for in_type, out_type in ((Nifti1Header, Nifti2Header), (Nifti1PairHeader, Nifti2Header), (Nifti1PairHeader, Nifti2PairHeader), (Nifti2Header, Nifti1Header), (Nifti2PairHeader, Nifti1Header), (Nifti2PairHeader, Nifti1PairHeader)):
    in_hdr = in_type()
    in_hdr.set_data_shape(shape)
    in_hdr.set_data_dtype(dtype_type)
    in_hdr.extensions[:] = [ext1, ext2]
    out_hdr = out_type.from_header(in_hdr)
    assert out_hdr.get_data_shape() == shape
    assert out_hdr.get_data_dtype() == dtype_type
    assert in_hdr.extensions == out_hdr.extensions
```

## Next Steps


---

*Source: test_nifti2.py:95 | Complexity: Advanced | Last updated: 2026-05-18*