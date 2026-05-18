# How To: Orientation

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test orientation

## Prerequisites

**Required Modules:**
- `os`
- `re`
- `logging`
- `pickle`
- `numpy`
- `py3k`
- `volumeutils`
- `spatialimages`
- `analyze`
- `nifti1`
- `loadsave`
- `casting`
- `numpy.testing`
- `testing`
- `test_wrapstruct`


## Step-by-Step Guide

### Step 1: Assign hdr = self.header_class(...)

```python
hdr = self.header_class()
```

**Verification:**
```python
assert_true(hdr.default_x_flip)
```

### Step 2: Call assert_true()

```python
assert_true(hdr.default_x_flip)
```

**Verification:**
```python
assert_array_equal(hdr.get_base_affine(), aff)
```

### Step 3: Call hdr.set_data_shape()

```python
hdr.set_data_shape((3, 5, 7))
```

**Verification:**
```python
assert_false(hdr.default_x_flip)
```

### Step 4: Call hdr.set_zooms()

```python
hdr.set_zooms((4, 5, 6))
```

**Verification:**
```python
assert_array_equal(hdr.get_base_affine(), aff)
```

### Step 5: Assign aff = np.diag(...)

```python
aff = np.diag((-4, 5, 6, 1))
```

### Step 6: Assign unknown = value

```python
aff[:3, 3] = np.array([1, 2, 3]) * np.array([-4, 5, 6]) * -1
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(hdr.get_base_affine(), aff)
```

### Step 8: Assign hdr.default_x_flip = False

```python
hdr.default_x_flip = False
```

### Step 9: Call assert_false()

```python
assert_false(hdr.default_x_flip)
```

### Step 10: Call assert_array_equal()

```python
assert_array_equal(hdr.get_base_affine(), aff)
```


## Complete Example

```python
# Workflow
hdr = self.header_class()
assert_true(hdr.default_x_flip)
hdr.set_data_shape((3, 5, 7))
hdr.set_zooms((4, 5, 6))
aff = np.diag((-4, 5, 6, 1))
aff[:3, 3] = np.array([1, 2, 3]) * np.array([-4, 5, 6]) * -1
assert_array_equal(hdr.get_base_affine(), aff)
hdr.default_x_flip = False
assert_false(hdr.default_x_flip)
aff[0] *= -1
assert_array_equal(hdr.get_base_affine(), aff)
```

## Next Steps


---

*Source: test_analyze.py:394 | Complexity: Advanced | Last updated: 2026-05-18*