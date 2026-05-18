# How To: Origin Affine

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test origin affine

## Prerequisites

**Required Modules:**
- `itertools`
- `unittest`
- `io`
- `numpy`
- `pytest`
- `numpy.testing`
- `optpkg`
- `casting`
- `spatialimages`
- `spm99analyze`
- `testing`
- `volumeutils`
- `scipy.io`


## Step-by-Step Guide

### Step 1: Assign hdr = Spm99AnalyzeHeader(...)

```python
hdr = Spm99AnalyzeHeader()
```

**Verification:**
```python
assert_array_equal(aff, hdr.get_base_affine())
```

### Step 2: Assign aff = hdr.get_origin_affine(...)

```python
aff = hdr.get_origin_affine()
```

**Verification:**
```python
assert hdr.default_x_flip
```

### Step 3: Call assert_array_equal()

```python
assert_array_equal(aff, hdr.get_base_affine())
```

**Verification:**
```python
assert_array_almost_equal(hdr.get_origin_affine(), [[-3.0, 0.0, 0.0, 3.0], [0.0, 2.0, 0.0, -4.0], [0.0, 0.0, 1.0, -3.0], [0.0, 0.0, 0.0, 1.0]])
```

### Step 4: Call hdr.set_data_shape()

```python
hdr.set_data_shape((3, 5, 7))
```

**Verification:**
```python
assert_array_almost_equal(hdr.get_origin_affine(), [[-3.0, 0.0, 0.0, 6.0], [0.0, 2.0, 0.0, -6.0], [0.0, 0.0, 1.0, -4.0], [0.0, 0.0, 0.0, 1.0]])
```

### Step 5: Call hdr.set_zooms()

```python
hdr.set_zooms((3, 2, 1))
```

**Verification:**
```python
assert_array_almost_equal(hdr.get_origin_affine(), [[-3.0, 0.0, 0.0, 3.0], [0.0, 2.0, 0.0, -4.0], [0.0, 0.0, 1.0, -0.0], [0.0, 0.0, 0.0, 1.0]])
```

### Step 6: Call assert_array_almost_equal()

```python
assert_array_almost_equal(hdr.get_origin_affine(), [[-3.0, 0.0, 0.0, 3.0], [0.0, 2.0, 0.0, -4.0], [0.0, 0.0, 1.0, -3.0], [0.0, 0.0, 0.0, 1.0]])
```

**Verification:**
```python
assert_array_almost_equal(hdr.get_origin_affine(), [[-3.0, 0.0, 0.0, 3.0], [0.0, 2.0, 0.0, -4.0], [0.0, 0.0, 1.0, -3.0], [0.0, 0.0, 0.0, 1.0]])
```

### Step 7: Assign unknown = value

```python
hdr['origin'][:3] = [3, 4, 5]
```

### Step 8: Call assert_array_almost_equal()

```python
assert_array_almost_equal(hdr.get_origin_affine(), [[-3.0, 0.0, 0.0, 6.0], [0.0, 2.0, 0.0, -6.0], [0.0, 0.0, 1.0, -4.0], [0.0, 0.0, 0.0, 1.0]])
```

### Step 9: Assign unknown = 0

```python
hdr['origin'] = 0
```

### Step 10: Call hdr.set_data_shape()

```python
hdr.set_data_shape((3, 5))
```

### Step 11: Call assert_array_almost_equal()

```python
assert_array_almost_equal(hdr.get_origin_affine(), [[-3.0, 0.0, 0.0, 3.0], [0.0, 2.0, 0.0, -4.0], [0.0, 0.0, 1.0, -0.0], [0.0, 0.0, 0.0, 1.0]])
```

### Step 12: Call hdr.set_data_shape()

```python
hdr.set_data_shape((3, 5, 7))
```

### Step 13: Call assert_array_almost_equal()

```python
assert_array_almost_equal(hdr.get_origin_affine(), [[-3.0, 0.0, 0.0, 3.0], [0.0, 2.0, 0.0, -4.0], [0.0, 0.0, 1.0, -3.0], [0.0, 0.0, 0.0, 1.0]])
```


## Complete Example

```python
# Workflow
hdr = Spm99AnalyzeHeader()
aff = hdr.get_origin_affine()
assert_array_equal(aff, hdr.get_base_affine())
hdr.set_data_shape((3, 5, 7))
hdr.set_zooms((3, 2, 1))
assert hdr.default_x_flip
assert_array_almost_equal(hdr.get_origin_affine(), [[-3.0, 0.0, 0.0, 3.0], [0.0, 2.0, 0.0, -4.0], [0.0, 0.0, 1.0, -3.0], [0.0, 0.0, 0.0, 1.0]])
hdr['origin'][:3] = [3, 4, 5]
assert_array_almost_equal(hdr.get_origin_affine(), [[-3.0, 0.0, 0.0, 6.0], [0.0, 2.0, 0.0, -6.0], [0.0, 0.0, 1.0, -4.0], [0.0, 0.0, 0.0, 1.0]])
hdr['origin'] = 0
hdr.set_data_shape((3, 5))
assert_array_almost_equal(hdr.get_origin_affine(), [[-3.0, 0.0, 0.0, 3.0], [0.0, 2.0, 0.0, -4.0], [0.0, 0.0, 1.0, -0.0], [0.0, 0.0, 0.0, 1.0]])
hdr.set_data_shape((3, 5, 7))
assert_array_almost_equal(hdr.get_origin_affine(), [[-3.0, 0.0, 0.0, 3.0], [0.0, 2.0, 0.0, -4.0], [0.0, 0.0, 1.0, -3.0], [0.0, 0.0, 0.0, 1.0]])
```

## Next Steps


---

*Source: test_spm99analyze.py:486 | Complexity: Advanced | Last updated: 2026-05-18*