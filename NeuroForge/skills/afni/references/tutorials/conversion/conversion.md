# How To: Conversion

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test conversion

## Prerequisites

**Required Modules:**
- `__future__`
- `os.path`
- `shutil`
- `tempfile`
- `py3k`
- `numpy`
- `tmpdirs`
- `volumeutils`
- `numpy.testing`
- `nose.tools`
- `scipy.io`


## Step-by-Step Guide

### Step 1: Assign shape = value

```python
shape = (2, 4, 6)
```

**Verification:**
```python
assert_array_equal(img2.get_data(), data)
```

### Step 2: Assign affine = np.diag(...)

```python
affine = np.diag([1, 2, 3, 1])
```

**Verification:**
```python
assert_array_equal(img2.get_affine(), affine)
```

### Step 3: Assign data = np.arange.reshape(...)

```python
data = np.arange(np.prod(shape), dtype=npt).reshape(shape)
```

### Step 4: Assign r_class = value

```python
r_class = r_class_def['class']
```

### Step 5: Assign img = r_class(...)

```python
img = r_class(data, affine)
```

### Step 6: Call img.set_data_dtype()

```python
img.set_data_dtype(npt)
```

### Step 7: Assign w_class = value

```python
w_class = w_class_def['class']
```

### Step 8: Assign img2 = w_class.from_image(...)

```python
img2 = w_class.from_image(img)
```

### Step 9: Call assert_array_equal()

```python
assert_array_equal(img2.get_data(), data)
```

### Step 10: Call assert_array_equal()

```python
assert_array_equal(img2.get_affine(), affine)
```


## Complete Example

```python
# Workflow
shape = (2, 4, 6)
affine = np.diag([1, 2, 3, 1])
for npt in (np.float32, np.int16):
    data = np.arange(np.prod(shape), dtype=npt).reshape(shape)
    for r_class_def in class_map.values():
        r_class = r_class_def['class']
        img = r_class(data, affine)
        img.set_data_dtype(npt)
        for w_class_def in class_map.values():
            w_class = w_class_def['class']
            img2 = w_class.from_image(img)
            assert_array_equal(img2.get_data(), data)
            assert_array_equal(img2.get_affine(), affine)
```

## Next Steps


---

*Source: test_image_load_save.py:52 | Complexity: Advanced | Last updated: 2026-05-18*