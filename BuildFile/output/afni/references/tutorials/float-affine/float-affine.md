# How To: Float Affine

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test float affine

## Prerequisites

**Required Modules:**
- `py3k`
- `numpy`
- `spatialimages`
- `unittest`
- `nose.tools`
- `numpy.testing`


## Step-by-Step Guide

### Step 1: Assign img_klass = value

```python
img_klass = self.image_class
```

**Verification:**
```python
assert_equal(img.get_affine().dtype, np.dtype(np.float64))
```

### Step 2: Assign arr = np.arange(...)

```python
arr = np.arange(3, dtype=np.int16)
```

**Verification:**
```python
assert_equal(img.get_affine().dtype, np.dtype(np.float64))
```

### Step 3: Assign img = img_klass(...)

```python
img = img_klass(arr, np.eye(4, dtype=np.float32))
```

### Step 4: Call assert_equal()

```python
assert_equal(img.get_affine().dtype, np.dtype(np.float64))
```

### Step 5: Assign img = img_klass(...)

```python
img = img_klass(arr, np.eye(4, dtype=np.int16))
```

### Step 6: Call assert_equal()

```python
assert_equal(img.get_affine().dtype, np.dtype(np.float64))
```


## Complete Example

```python
# Workflow
img_klass = self.image_class
arr = np.arange(3, dtype=np.int16)
img = img_klass(arr, np.eye(4, dtype=np.float32))
assert_equal(img.get_affine().dtype, np.dtype(np.float64))
img = img_klass(arr, np.eye(4, dtype=np.int16))
assert_equal(img.get_affine().dtype, np.dtype(np.float64))
```

## Next Steps


---

*Source: test_spatialimages.py:197 | Complexity: Intermediate | Last updated: 2026-05-18*