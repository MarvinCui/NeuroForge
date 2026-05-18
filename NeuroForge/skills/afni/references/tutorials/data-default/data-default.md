# How To: Data Default

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test data default

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
assert_equal(data.dtype, img.get_data_dtype())
```

### Step 2: Assign hdr_klass = value

```python
hdr_klass = self.image_class.header_class
```

**Verification:**
```python
assert_equal(img.get_data_dtype(), np.dtype(np.float32))
```

### Step 3: Assign data = np.arange.reshape(...)

```python
data = np.arange(24, dtype=np.int32).reshape((2, 3, 4))
```

### Step 4: Assign affine = np.eye(...)

```python
affine = np.eye(4)
```

### Step 5: Assign img = img_klass(...)

```python
img = img_klass(data, affine)
```

### Step 6: Call assert_equal()

```python
assert_equal(data.dtype, img.get_data_dtype())
```

### Step 7: Assign header = hdr_klass(...)

```python
header = hdr_klass()
```

### Step 8: Assign img = img_klass(...)

```python
img = img_klass(data, affine, header)
```

### Step 9: Call assert_equal()

```python
assert_equal(img.get_data_dtype(), np.dtype(np.float32))
```


## Complete Example

```python
# Workflow
img_klass = self.image_class
hdr_klass = self.image_class.header_class
data = np.arange(24, dtype=np.int32).reshape((2, 3, 4))
affine = np.eye(4)
img = img_klass(data, affine)
assert_equal(data.dtype, img.get_data_dtype())
header = hdr_klass()
img = img_klass(data, affine, header)
assert_equal(img.get_data_dtype(), np.dtype(np.float32))
```

## Next Steps


---

*Source: test_spatialimages.py:224 | Complexity: Advanced | Last updated: 2026-05-18*