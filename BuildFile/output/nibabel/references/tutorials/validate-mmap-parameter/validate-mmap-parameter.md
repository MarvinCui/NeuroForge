# How To: Validate Mmap Parameter

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, unittest, workflow, integration

## Overview

Workflow: validate mmap parameter

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `io`
- `pathlib`
- `sys`
- `warnings`
- `functools`
- `itertools`
- `numpy`
- `optpkg`
- `unittest`
- `pytest`
- `numpy.testing`
- `nibabel.arraywriters`
- `nibabel.testing`
- `casting`
- `spatialimages`
- `tmpdirs`
- `test_api_validators`
- `test_brikhead`
- `test_minc1`
- `test_minc2`
- `test_parrec`
- `uuid`

**Setup Required:**
```python
# Fixtures: imaker, params
```

## Step-by-Step Guide

### Step 1: Assign img = imaker(...)

```python
img = imaker()
```

**Verification:**
```python
assert_almost_equal(img.get_fdata(), rt_img.get_fdata())
```

### Step 2: Assign fname = img.get_filename(...)

```python
fname = img.get_filename()
```

**Verification:**
```python
assert_almost_equal(img.get_fdata(), rt_img.get_fdata())
```

### Step 3: Assign rt_img = img.__class__.from_filename(...)

```python
rt_img = img.__class__.from_filename(fname, mmap=True)
```

**Verification:**
```python
assert_almost_equal(img.get_fdata(), rt_img.get_fdata())
```

### Step 4: Call assert_almost_equal()

```python
assert_almost_equal(img.get_fdata(), rt_img.get_fdata())
```

**Verification:**
```python
assert_almost_equal(img.get_fdata(), rt_img.get_fdata())
```

### Step 5: Assign rt_img = img.__class__.from_filename(...)

```python
rt_img = img.__class__.from_filename(fname, mmap=False)
```

### Step 6: Call assert_almost_equal()

```python
assert_almost_equal(img.get_fdata(), rt_img.get_fdata())
```

### Step 7: Assign rt_img = img.__class__.from_filename(...)

```python
rt_img = img.__class__.from_filename(fname, mmap='c')
```

### Step 8: Call assert_almost_equal()

```python
assert_almost_equal(img.get_fdata(), rt_img.get_fdata())
```

### Step 9: Assign rt_img = img.__class__.from_filename(...)

```python
rt_img = img.__class__.from_filename(fname, mmap='r')
```

### Step 10: Call assert_almost_equal()

```python
assert_almost_equal(img.get_fdata(), rt_img.get_fdata())
```

### Step 11: Assign fname = value

```python
fname = 'image' + img.valid_exts[0]
```

### Step 12: Call img.to_filename()

```python
img.to_filename(fname)
```

### Step 13: Call img.__class__.from_filename()

```python
img.__class__.from_filename(fname, mmap='r+')
```

### Step 14: Call img.__class__.from_filename()

```python
img.__class__.from_filename(fname, mmap='invalid')
```


## Complete Example

```python
# Setup
# Fixtures: imaker, params

# Workflow
img = imaker()
fname = img.get_filename()
with InTemporaryDirectory():
    if fname is None:
        if not img.rw or not img.valid_exts:
            return
        fname = 'image' + img.valid_exts[0]
        img.to_filename(fname)
    rt_img = img.__class__.from_filename(fname, mmap=True)
    assert_almost_equal(img.get_fdata(), rt_img.get_fdata())
    rt_img = img.__class__.from_filename(fname, mmap=False)
    assert_almost_equal(img.get_fdata(), rt_img.get_fdata())
    rt_img = img.__class__.from_filename(fname, mmap='c')
    assert_almost_equal(img.get_fdata(), rt_img.get_fdata())
    rt_img = img.__class__.from_filename(fname, mmap='r')
    assert_almost_equal(img.get_fdata(), rt_img.get_fdata())
    with pytest.raises(ValueError):
        img.__class__.from_filename(fname, mmap='r+')
    with pytest.raises(ValueError):
        img.__class__.from_filename(fname, mmap='invalid')
    del rt_img
```

## Next Steps


---

*Source: test_image_api.py:425 | Complexity: Advanced | Last updated: 2026-05-18*