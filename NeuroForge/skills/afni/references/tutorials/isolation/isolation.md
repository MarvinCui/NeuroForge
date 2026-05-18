# How To: Isolation

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test isolation

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
assert_array_equal(img.get_affine(), aff)
```

### Step 2: Assign arr = np.arange(...)

```python
arr = np.arange(3, dtype=np.int16)
```

**Verification:**
```python
assert_false(np.all(img.get_affine() == aff))
```

### Step 3: Assign aff = np.eye(...)

```python
aff = np.eye(4)
```

**Verification:**
```python
assert_not_equal(img.get_header(), ihdr)
```

### Step 4: Assign img = img_klass(...)

```python
img = img_klass(arr, aff)
```

### Step 5: Call assert_array_equal()

```python
assert_array_equal(img.get_affine(), aff)
```

### Step 6: Assign unknown = 99

```python
aff[0, 0] = 99
```

### Step 7: Call assert_false()

```python
assert_false(np.all(img.get_affine() == aff))
```

### Step 8: Assign ihdr = img.get_header(...)

```python
ihdr = img.get_header()
```

### Step 9: Assign img = img_klass(...)

```python
img = img_klass(arr, aff, ihdr)
```

### Step 10: Call ihdr.set_zooms()

```python
ihdr.set_zooms((4,))
```

### Step 11: Call assert_not_equal()

```python
assert_not_equal(img.get_header(), ihdr)
```


## Complete Example

```python
# Workflow
img_klass = self.image_class
arr = np.arange(3, dtype=np.int16)
aff = np.eye(4)
img = img_klass(arr, aff)
assert_array_equal(img.get_affine(), aff)
aff[0, 0] = 99
assert_false(np.all(img.get_affine() == aff))
ihdr = img.get_header()
img = img_klass(arr, aff, ihdr)
ihdr.set_zooms((4,))
assert_not_equal(img.get_header(), ihdr)
```

## Next Steps


---

*Source: test_spatialimages.py:180 | Complexity: Advanced | Last updated: 2026-05-18*