# How To: Validate Filenames

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, unittest, workflow, integration

## Overview

Workflow: validate filenames

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
assert_array_equal(img.shape, rt_img.shape)
```

### Step 2: Call img.set_data_dtype()

```python
img.set_data_dtype(np.float32)
```

**Verification:**
```python
assert_almost_equal(img.get_fdata(), rt_img.get_fdata())
```

### Step 3: Assign img.file_map = None

```python
img.file_map = None
```

**Verification:**
```python
assert_almost_equal(np.asanyarray(img.dataobj), np.asanyarray(rt_img.dataobj))
```

### Step 4: Assign rt_img = bytesio_round_trip(...)

```python
rt_img = bytesio_round_trip(img)
```

**Verification:**
```python
assert_almost_equal(img.get_fdata(), rt_rt_img.get_fdata())
```

### Step 5: Call assert_array_equal()

```python
assert_array_equal(img.shape, rt_img.shape)
```

**Verification:**
```python
assert_almost_equal(np.asanyarray(img.dataobj), np.asanyarray(rt_img.dataobj))
```

### Step 6: Call assert_almost_equal()

```python
assert_almost_equal(img.get_fdata(), rt_img.get_fdata())
```

**Verification:**
```python
assert img.get_filename() == str(path)
```

### Step 7: Call assert_almost_equal()

```python
assert_almost_equal(np.asanyarray(img.dataobj), np.asanyarray(rt_img.dataobj))
```

**Verification:**
```python
assert img.file_map['image'].filename == str(path)
```

### Step 8: Assign klass = type(...)

```python
klass = type(img)
```

**Verification:**
```python
assert_array_equal(img.shape, rt_img.shape)
```

### Step 9: Assign rt_img.file_map = bytesio_filemap(...)

```python
rt_img.file_map = bytesio_filemap(klass)
```

**Verification:**
```python
assert_almost_equal(img.get_fdata(), rt_img.get_fdata())
```

### Step 10: Call rt_img.to_file_map()

```python
rt_img.to_file_map()
```

**Verification:**
```python
assert_almost_equal(np.asanyarray(img.dataobj), np.asanyarray(rt_img.dataobj))
```

### Step 11: Assign rt_rt_img = klass.from_file_map(...)

```python
rt_rt_img = klass.from_file_map(rt_img.file_map)
```

### Step 12: Call assert_almost_equal()

```python
assert_almost_equal(img.get_fdata(), rt_rt_img.get_fdata())
```

### Step 13: Call assert_almost_equal()

```python
assert_almost_equal(np.asanyarray(img.dataobj), np.asanyarray(rt_img.dataobj))
```

### Step 14: Assign fname = value

```python
fname = 'an_image' + self.standard_extension
```

### Step 15: Assign fname = value

```python
fname = 'another_image' + self.standard_extension
```

### Step 16: Call img.set_filename()

```python
img.set_filename(path)
```

**Verification:**
```python
assert img.get_filename() == str(path)
```

### Step 17: Call assert_array_equal()

```python
assert_array_equal(img.shape, rt_img.shape)
```

### Step 18: Call assert_almost_equal()

```python
assert_almost_equal(img.get_fdata(), rt_img.get_fdata())
```

### Step 19: Call assert_almost_equal()

```python
assert_almost_equal(np.asanyarray(img.dataobj), np.asanyarray(rt_img.dataobj))
```

### Step 20: Call warnings.filterwarnings()

```python
warnings.filterwarnings('error', category=DeprecationWarning, module='nibabel.*')
```

### Step 21: Call img.to_filename()

```python
img.to_filename(path)
```

### Step 22: Assign rt_img = img.__class__.from_filename(...)

```python
rt_img = img.__class__.from_filename(path)
```


## Complete Example

```python
# Setup
# Fixtures: imaker, params

# Workflow
if not self.can_save:
    raise unittest.SkipTest
img = imaker()
img.set_data_dtype(np.float32)
img.file_map = None
rt_img = bytesio_round_trip(img)
assert_array_equal(img.shape, rt_img.shape)
assert_almost_equal(img.get_fdata(), rt_img.get_fdata())
assert_almost_equal(np.asanyarray(img.dataobj), np.asanyarray(rt_img.dataobj))
klass = type(img)
rt_img.file_map = bytesio_filemap(klass)
rt_img.to_file_map()
rt_rt_img = klass.from_file_map(rt_img.file_map)
assert_almost_equal(img.get_fdata(), rt_rt_img.get_fdata())
assert_almost_equal(np.asanyarray(img.dataobj), np.asanyarray(rt_img.dataobj))
fname = 'an_image' + self.standard_extension
for path in (fname, pathlib.Path(fname)):
    img.set_filename(path)
    assert img.get_filename() == str(path)
    assert img.file_map['image'].filename == str(path)
fname = 'another_image' + self.standard_extension
for path in (fname, pathlib.Path(fname)):
    with InTemporaryDirectory():
        with clear_and_catch_warnings():
            warnings.filterwarnings('error', category=DeprecationWarning, module='nibabel.*')
            img.to_filename(path)
            rt_img = img.__class__.from_filename(path)
        assert_array_equal(img.shape, rt_img.shape)
        assert_almost_equal(img.get_fdata(), rt_img.get_fdata())
        assert_almost_equal(np.asanyarray(img.dataobj), np.asanyarray(rt_img.dataobj))
        del rt_img
```

## Next Steps


---

*Source: test_image_api.py:140 | Complexity: Advanced | Last updated: 2026-05-18*