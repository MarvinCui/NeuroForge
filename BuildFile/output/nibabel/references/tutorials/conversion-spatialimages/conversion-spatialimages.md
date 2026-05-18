# How To: Conversion Spatialimages

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test conversion spatialimages

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `logging`
- `pathlib`
- `shutil`
- `io`
- `os.path`
- `os.path`
- `tempfile`
- `numpy`
- `pytest`
- `numpy.testing`
- `optpkg`
- `spatialimages`
- `testing`
- `tmpdirs`
- `volumeutils`

**Setup Required:**
```python
# Fixtures: caplog
```

## Step-by-Step Guide

### Step 1: Assign shape = value

```python
shape = (2, 4, 6)
```

**Verification:**
```python
assert_array_equal(img2.get_fdata(), data)
```

### Step 2: Assign affine = np.diag(...)

```python
affine = np.diag([1, 2, 3, 1])
```

**Verification:**
```python
assert_array_equal(img2.affine, affine)
```

### Step 3: Assign klasses = value

```python
klasses = [klass for klass in all_image_classes if klass.rw and issubclass(klass, SpatialImage)]
```

### Step 4: Assign data = np.arange.reshape(...)

```python
data = np.arange(np.prod(shape), dtype=npt).reshape(shape)
```

### Step 5: Assign img = r_class(...)

```python
img = r_class(data, affine)
```

### Step 6: Call img.set_data_dtype()

```python
img.set_data_dtype(npt)
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(img2.get_fdata(), data)
```

### Step 8: Call assert_array_equal()

```python
assert_array_equal(img2.affine, affine)
```

### Step 9: Assign img2 = w_class.from_image(...)

```python
img2 = w_class.from_image(img)
```


## Complete Example

```python
# Setup
# Fixtures: caplog

# Workflow
shape = (2, 4, 6)
affine = np.diag([1, 2, 3, 1])
klasses = [klass for klass in all_image_classes if klass.rw and issubclass(klass, SpatialImage)]
for npt in (np.float32, np.int16):
    data = np.arange(np.prod(shape), dtype=npt).reshape(shape)
    for r_class in klasses:
        if not r_class.makeable:
            continue
        img = r_class(data, affine)
        img.set_data_dtype(npt)
        for w_class in klasses:
            if not w_class.makeable:
                continue
            with caplog.at_level(logging.CRITICAL):
                img2 = w_class.from_image(img)
            assert_array_equal(img2.get_fdata(), data)
            assert_array_equal(img2.affine, affine)
```

## Next Steps


---

*Source: test_image_load_save.py:57 | Complexity: Advanced | Last updated: 2026-05-18*