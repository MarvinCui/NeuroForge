# How To: Float Affine

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test float affine

## Prerequisites

**Required Modules:**
- `os`
- `pathlib`
- `unittest`
- `numpy`
- `pytest`
- `numpy.testing`
- `ecat`
- `openers`
- `testing`
- `tmpdirs`
- `test_fileslice`


## Step-by-Step Guide

### Step 1: Assign img_klass = value

```python
img_klass = self.image_class
```

**Verification:**
```python
assert img.affine.dtype == np.dtype(np.float64)
```

### Step 2: Assign unknown = value

```python
arr, aff, hdr, sub_hdr, mlist = (self.img.get_fdata(), self.img.affine, self.img.header, self.img.get_subheaders(), self.img.get_mlist())
```

**Verification:**
```python
assert img.affine.dtype == np.dtype(np.float64)
```

### Step 3: Assign img = img_klass(...)

```python
img = img_klass(arr, aff.astype(np.float32), hdr, sub_hdr, mlist)
```

**Verification:**
```python
assert img.affine.dtype == np.dtype(np.float64)
```

### Step 4: Assign img = img_klass(...)

```python
img = img_klass(arr, aff.astype(np.int16), hdr, sub_hdr, mlist)
```

**Verification:**
```python
assert img.affine.dtype == np.dtype(np.float64)
```


## Complete Example

```python
# Workflow
img_klass = self.image_class
arr, aff, hdr, sub_hdr, mlist = (self.img.get_fdata(), self.img.affine, self.img.header, self.img.get_subheaders(), self.img.get_mlist())
img = img_klass(arr, aff.astype(np.float32), hdr, sub_hdr, mlist)
assert img.affine.dtype == np.dtype(np.float64)
img = img_klass(arr, aff.astype(np.int16), hdr, sub_hdr, mlist)
assert img.affine.dtype == np.dtype(np.float64)
```

## Next Steps


---

*Source: test_ecat.py:243 | Complexity: Intermediate | Last updated: 2026-05-18*