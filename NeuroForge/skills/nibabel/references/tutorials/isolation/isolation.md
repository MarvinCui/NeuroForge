# How To: Isolation

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, unittest, workflow, integration

## Overview

Workflow: test isolation

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
assert_array_equal(img.affine, aff)
```

### Step 2: Assign unknown = value

```python
arr, aff, hdr, sub_hdr, mlist = (self.img.get_fdata(), self.img.affine, self.img.header, self.img.get_subheaders(), self.img.get_mlist())
```

**Verification:**
```python
assert not np.all(img.affine == aff)
```

### Step 3: Assign img = img_klass(...)

```python
img = img_klass(arr, aff, hdr, sub_hdr, mlist)
```

### Step 4: Call assert_array_equal()

```python
assert_array_equal(img.affine, aff)
```

### Step 5: Assign unknown = 99

```python
aff[0, 0] = 99
```

**Verification:**
```python
assert not np.all(img.affine == aff)
```


## Complete Example

```python
# Workflow
img_klass = self.image_class
arr, aff, hdr, sub_hdr, mlist = (self.img.get_fdata(), self.img.affine, self.img.header, self.img.get_subheaders(), self.img.get_mlist())
img = img_klass(arr, aff, hdr, sub_hdr, mlist)
assert_array_equal(img.affine, aff)
aff[0, 0] = 99
assert not np.all(img.affine == aff)
```

## Next Steps


---

*Source: test_ecat.py:228 | Complexity: Intermediate | Last updated: 2026-05-18*