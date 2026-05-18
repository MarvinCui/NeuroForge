# How To: Load Mmap

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test load mmap

## Prerequisites

**Required Modules:**
- `io`
- `numpy`
- `pytest`
- `numpy.testing`
- `imageclasses`
- `spatialimages`
- `testing`
- `tmpdirs`


## Step-by-Step Guide

### Step 1: Assign img_klass = value

```python
img_klass = self.image_class
```

**Verification:**
```python
assert not isinstance(back_data, np.memmap), f'Should not be a {img_klass.__name__}'
```

### Step 2: Assign viral_memmap = memmap_after_ufunc(...)

```python
viral_memmap = memmap_after_ufunc()
```

**Verification:**
```python
assert isinstance(back_data, np.memmap), f'Not a {img_klass.__name__}'
```

### Step 3: Assign unknown = self.get_disk_image(...)

```python
img, fname, has_scaling = self.get_disk_image()
```

**Verification:**
```python
assert back_data.mode == expected_mode
```

### Step 4: Assign file_map = img.file_map.copy(...)

```python
file_map = img.file_map.copy()
```

### Step 5: Assign kwargs = value

```python
kwargs = {}
```

### Step 6: Assign back_img = func(...)

```python
back_img = func(param1, **kwargs)
```

### Step 7: Assign back_data = np.asanyarray(...)

```python
back_data = np.asanyarray(back_img.dataobj)
```

### Step 8: Call func()

```python
func(param1, True)
```

### Step 9: Call func()

```python
func(param1, mmap='rw')
```

### Step 10: Call func()

```python
func(param1, mmap='r+')
```

### Step 11: Assign expected_mode = None

```python
expected_mode = None
```

### Step 12: Assign unknown = mmap

```python
kwargs['mmap'] = mmap
```

**Verification:**
```python
assert not isinstance(back_data, np.memmap), f'Should not be a {img_klass.__name__}'
```


## Complete Example

```python
# Workflow
img_klass = self.image_class
viral_memmap = memmap_after_ufunc()
with InTemporaryDirectory():
    img, fname, has_scaling = self.get_disk_image()
    file_map = img.file_map.copy()
    for func, param1 in ((img_klass.from_filename, fname), (img_klass.load, fname), (top_load, fname), (img_klass.from_file_map, file_map)):
        for mmap, expected_mode in ((None, 'c'), (True, 'c'), ('c', 'c'), ('r', 'r'), (False, None)):
            if has_scaling and (not viral_memmap):
                expected_mode = None
            kwargs = {}
            if mmap is not None:
                kwargs['mmap'] = mmap
            back_img = func(param1, **kwargs)
            back_data = np.asanyarray(back_img.dataobj)
            if expected_mode is None:
                assert not isinstance(back_data, np.memmap), f'Should not be a {img_klass.__name__}'
            else:
                assert isinstance(back_data, np.memmap), f'Not a {img_klass.__name__}'
                if self.check_mmap_mode:
                    assert back_data.mode == expected_mode
            del back_img, back_data
        with pytest.raises(TypeError):
            func(param1, True)
        with pytest.raises(ValueError):
            func(param1, mmap='rw')
        with pytest.raises(ValueError):
            func(param1, mmap='r+')
```

## Next Steps


---

*Source: test_spatialimages.py:578 | Complexity: Advanced | Last updated: 2026-05-18*