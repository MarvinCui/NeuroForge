# How To: Check Img Dtype

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test check img dtype

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.direction.peaks`
- `dipy.testing.decorators`
- `dipy.viz.horizon.util`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign affine = np.array(...)

```python
affine = np.array([[1.0, 0.0, 0.0, -98.0], [0.0, 1.0, 0.0, -134.0], [0.0, 0.0, 1.0, -72.0], [0.0, 0.0, 0.0, 1.0]])
```

**Verification:**
```python
assert len(check_img_dtype(images)) == 1
```

### Step 2: Assign data = value

```python
data = 255 * rng.random((197, 233, 189))
```

**Verification:**
```python
assert len(check_img_dtype(images)) == 1
```

### Step 3: Assign images = value

```python
images = [(data, affine)]
```

**Verification:**
```python
assert len(check_img_dtype(images)) == 0
```

### Step 4: Call npt.assert_equal()

```python
npt.assert_equal(check_img_dtype(images)[0], images[0])
```

### Step 5: Assign data = rng.random.astype(...)

```python
data = rng.random((5, 5, 5)).astype(np.int64)
```

### Step 6: Assign images = value

```python
images = [(data, affine)]
```

### Step 7: Call npt.assert_equal()

```python
npt.assert_equal(check_img_dtype(images)[0][0].dtype, np.int32)
```

**Verification:**
```python
assert len(check_img_dtype(images)) == 1
```

### Step 8: Assign data = rng.random.astype(...)

```python
data = rng.random((5, 5, 5)).astype(np.float16)
```

### Step 9: Assign images = value

```python
images = [(data, affine)]
```

### Step 10: Call npt.assert_equal()

```python
npt.assert_equal(check_img_dtype(images)[0][0].dtype, np.float32)
```

**Verification:**
```python
assert len(check_img_dtype(images)) == 1
```

### Step 11: Assign data = rng.random.astype(...)

```python
data = rng.random((5, 5, 5)).astype(np.bool_)
```

### Step 12: Assign images = value

```python
images = [(data, affine)]
```

**Verification:**
```python
assert len(check_img_dtype(images)) == 0
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
affine = np.array([[1.0, 0.0, 0.0, -98.0], [0.0, 1.0, 0.0, -134.0], [0.0, 0.0, 1.0, -72.0], [0.0, 0.0, 0.0, 1.0]])
data = 255 * rng.random((197, 233, 189))
images = [(data, affine)]
npt.assert_equal(check_img_dtype(images)[0], images[0])
data = rng.random((5, 5, 5)).astype(np.int64)
images = [(data, affine)]
npt.assert_equal(check_img_dtype(images)[0][0].dtype, np.int32)
assert len(check_img_dtype(images)) == 1
data = rng.random((5, 5, 5)).astype(np.float16)
images = [(data, affine)]
npt.assert_equal(check_img_dtype(images)[0][0].dtype, np.float32)
assert len(check_img_dtype(images)) == 1
data = rng.random((5, 5, 5)).astype(np.bool_)
images = [(data, affine)]
assert len(check_img_dtype(images)) == 0
```

## Next Steps


---

*Source: test_util.py:68 | Complexity: Advanced | Last updated: 2026-05-18*