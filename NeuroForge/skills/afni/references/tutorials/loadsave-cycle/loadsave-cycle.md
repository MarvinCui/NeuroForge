# How To: Loadsave Cycle

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test loadsave cycle

## Prerequisites

**Required Modules:**
- `__future__`
- `os`
- `py3k`
- `numpy`
- `casting`
- `tmpdirs`
- `spatialimages`
- `affines`
- `nifti1`
- `test_arraywriters`
- `numpy.testing`
- `nose.tools`
- `nose`
- `testing`


## Step-by-Step Guide

### Step 1: Assign nim = load(...)

```python
nim = load(image_file)
```

**Verification:**
```python
assert_true(len(exts_container) > 0)
```

### Step 2: Assign hdr = nim.get_header(...)

```python
hdr = nim.get_header()
```

**Verification:**
```python
assert_equal(exts_container, lexts_container)
```

### Step 3: Assign exts_container = value

```python
exts_container = hdr.extensions
```

**Verification:**
```python
assert_equal(hdr.get_data_dtype(), np.int16)
```

### Step 4: Call assert_true()

```python
assert_true(len(exts_container) > 0)
```

**Verification:**
```python
assert_equal(hdr.get_slope_inter(), (1.0, 0.0))
```

### Step 5: Assign stio = BytesIO(...)

```python
stio = BytesIO()
```

**Verification:**
```python
assert_equal(hdr.get_slope_inter(), (2, 8))
```

### Step 6: Assign unknown.fileobj = stio

```python
nim.file_map['image'].fileobj = stio
```

**Verification:**
```python
assert_equal(wnim.get_data_dtype(), np.int16)
```

### Step 7: Call nim.to_file_map()

```python
nim.to_file_map()
```

**Verification:**
```python
assert_equal(wnim.get_header().get_slope_inter(), (2, 8))
```

### Step 8: Call stio.seek()

```python
stio.seek(0)
```

**Verification:**
```python
assert_equal(lnim.get_data_dtype(), np.int16)
```

### Step 9: Assign lnim = Nifti1Image.from_file_map(...)

```python
lnim = Nifti1Image.from_file_map(nim.file_map)
```

**Verification:**
```python
assert_equal(lnim.get_header().get_slope_inter(), (2, 8))
```

### Step 10: Assign hdr = lnim.get_header(...)

```python
hdr = lnim.get_header()
```

### Step 11: Assign lexts_container = value

```python
lexts_container = hdr.extensions
```

### Step 12: Call assert_equal()

```python
assert_equal(exts_container, lexts_container)
```

### Step 13: Assign data = np.ones(...)

```python
data = np.ones((2, 3, 4, 5), dtype='int16')
```

### Step 14: Assign img = Nifti1Image(...)

```python
img = Nifti1Image(data, np.eye(4))
```

### Step 15: Assign hdr = img.get_header(...)

```python
hdr = img.get_header()
```

### Step 16: Call assert_equal()

```python
assert_equal(hdr.get_data_dtype(), np.int16)
```

### Step 17: Call assert_equal()

```python
assert_equal(hdr.get_slope_inter(), (1.0, 0.0))
```

### Step 18: Call hdr.set_slope_inter()

```python
hdr.set_slope_inter(2, 8)
```

### Step 19: Call assert_equal()

```python
assert_equal(hdr.get_slope_inter(), (2, 8))
```

### Step 20: Assign wnim = Nifti1Image(...)

```python
wnim = Nifti1Image(data, np.eye(4), header=hdr)
```

### Step 21: Call assert_equal()

```python
assert_equal(wnim.get_data_dtype(), np.int16)
```

### Step 22: Call assert_equal()

```python
assert_equal(wnim.get_header().get_slope_inter(), (2, 8))
```

### Step 23: Assign stio = BytesIO(...)

```python
stio = BytesIO()
```

### Step 24: Assign unknown.fileobj = stio

```python
wnim.file_map['image'].fileobj = stio
```

### Step 25: Call wnim.to_file_map()

```python
wnim.to_file_map()
```

### Step 26: Call stio.seek()

```python
stio.seek(0)
```

### Step 27: Assign lnim = Nifti1Image.from_file_map(...)

```python
lnim = Nifti1Image.from_file_map(wnim.file_map)
```

### Step 28: Call assert_equal()

```python
assert_equal(lnim.get_data_dtype(), np.int16)
```

### Step 29: Call assert_equal()

```python
assert_equal(lnim.get_header().get_slope_inter(), (2, 8))
```


## Complete Example

```python
# Workflow
nim = load(image_file)
hdr = nim.get_header()
exts_container = hdr.extensions
assert_true(len(exts_container) > 0)
stio = BytesIO()
nim.file_map['image'].fileobj = stio
nim.to_file_map()
stio.seek(0)
lnim = Nifti1Image.from_file_map(nim.file_map)
hdr = lnim.get_header()
lexts_container = hdr.extensions
assert_equal(exts_container, lexts_container)
data = np.ones((2, 3, 4, 5), dtype='int16')
img = Nifti1Image(data, np.eye(4))
hdr = img.get_header()
assert_equal(hdr.get_data_dtype(), np.int16)
assert_equal(hdr.get_slope_inter(), (1.0, 0.0))
hdr.set_slope_inter(2, 8)
assert_equal(hdr.get_slope_inter(), (2, 8))
wnim = Nifti1Image(data, np.eye(4), header=hdr)
assert_equal(wnim.get_data_dtype(), np.int16)
assert_equal(wnim.get_header().get_slope_inter(), (2, 8))
stio = BytesIO()
wnim.file_map['image'].fileobj = stio
wnim.to_file_map()
stio.seek(0)
lnim = Nifti1Image.from_file_map(wnim.file_map)
assert_equal(lnim.get_data_dtype(), np.int16)
raise SkipTest
assert_equal(lnim.get_header().get_slope_inter(), (2, 8))
```

## Next Steps


---

*Source: test_nifti1.py:789 | Complexity: Advanced | Last updated: 2026-05-18*