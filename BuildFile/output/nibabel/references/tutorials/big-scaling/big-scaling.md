# How To: Big Scaling

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test big scaling

## Prerequisites

**Required Modules:**
- `os`
- `struct`
- `unittest`
- `warnings`
- `io`
- `numpy`
- `pytest`
- `numpy.testing`
- `nibabel`
- `nibabel.affines`
- `nibabel.casting`
- `nibabel.eulerangles`
- `nibabel.nifti1`
- `nibabel.optpkg`
- `nibabel.pkg_info`
- `nibabel.spatialimages`
- `nibabel.tmpdirs`
- `freesurfer`
- `orientations`
- `testing`
- `nibabel_data`
- `test_arraywriters`
- `test_orientations`
- `io`
- `json`


## Step-by-Step Guide

### Step 1: Assign hdr = self.header_class(...)

```python
hdr = self.header_class()
```

**Verification:**
```python
assert np.allclose(data, data_back)
```

### Step 2: Call hdr.set_data_shape()

```python
hdr.set_data_shape((2, 1, 1))
```

### Step 3: Call hdr.set_data_dtype()

```python
hdr.set_data_dtype(np.int16)
```

### Step 4: Assign sio = BytesIO(...)

```python
sio = BytesIO()
```

### Step 5: Assign dtt = value

```python
dtt = np.float32
```

### Step 6: Assign finf = type_info(...)

```python
finf = type_info(dtt)
```

### Step 7: Assign data = value

```python
data = np.array([finf['min'], finf['max']], dtype=dtt)[:, None, None]
```

### Step 8: Call hdr.data_to_fileobj()

```python
hdr.data_to_fileobj(data, sio)
```

### Step 9: Assign data_back = hdr.data_from_fileobj(...)

```python
data_back = hdr.data_from_fileobj(sio)
```

**Verification:**
```python
assert np.allclose(data, data_back)
```


## Complete Example

```python
# Workflow
hdr = self.header_class()
hdr.set_data_shape((2, 1, 1))
hdr.set_data_dtype(np.int16)
sio = BytesIO()
dtt = np.float32
finf = type_info(dtt)
data = np.array([finf['min'], finf['max']], dtype=dtt)[:, None, None]
hdr.data_to_fileobj(data, sio)
data_back = hdr.data_from_fileobj(sio)
assert np.allclose(data, data_back)
```

## Next Steps


---

*Source: test_nifti1.py:127 | Complexity: Advanced | Last updated: 2026-05-18*