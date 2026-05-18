# How To: Image Typing

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test image typing

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `itertools`
- `sys`
- `io`
- `numpy`
- `pytest`
- `numpy.testing`
- `nibabel.tmpdirs`
- `fileholders`
- `nifti1`
- `testing`
- `test_parse_gifti_fast`
- `gifti`

**Setup Required:**
```python
# Fixtures: label
```

## Step-by-Step Guide

### Step 1: Assign dtype = value

```python
dtype = data_type_codes.dtype[label]
```

**Verification:**
```python
assert np.array_equal(cast, force_rt.darrays[0].data)
```

### Step 2: Assign arr = value

```python
arr = 127 * rng.random(20)
```

**Verification:**
```python
assert np.allclose(cast, compat_darr)
```

### Step 3: Assign darr = GiftiDataArray(...)

```python
darr = GiftiDataArray(cast, datatype=label)
```

**Verification:**
```python
assert compat_darr.dtype in ('uint8', 'int32', 'float32')
```

### Step 4: Assign img = GiftiImage(...)

```python
img = GiftiImage(darrays=[darr])
```

**Verification:**
```python
assert np.array_equal(cast, strict_rt.darrays[0].data)
```

### Step 5: Assign force_rt = img.from_bytes(...)

```python
force_rt = img.from_bytes(img.to_bytes(mode='force'))
```

**Verification:**
```python
assert np.array_equal(cast, force_rt.darrays[0].data)
```

### Step 6: Assign cast = arr.astype(...)

```python
cast = arr.astype(label)
```

### Step 7: Assign compat_rt = img.from_bytes(...)

```python
compat_rt = img.from_bytes(img.to_bytes(mode='compat'))
```

### Step 8: Assign compat_darr = value

```python
compat_darr = compat_rt.darrays[0].data
```

**Verification:**
```python
assert np.allclose(cast, compat_darr)
```

### Step 9: Assign strict_rt = img.from_bytes(...)

```python
strict_rt = img.from_bytes(img.to_bytes(mode='strict'))
```

**Verification:**
```python
assert np.array_equal(cast, strict_rt.darrays[0].data)
```

### Step 10: Call img.to_bytes()

```python
img.to_bytes(mode='compat')
```

### Step 11: Call img.to_bytes()

```python
img.to_bytes(mode='strict')
```


## Complete Example

```python
# Setup
# Fixtures: label

# Workflow
dtype = data_type_codes.dtype[label]
if dtype == np.void:
    return
arr = 127 * rng.random(20)
try:
    cast = arr.astype(label)
except TypeError:
    return
darr = GiftiDataArray(cast, datatype=label)
img = GiftiImage(darrays=[darr])
force_rt = img.from_bytes(img.to_bytes(mode='force'))
assert np.array_equal(cast, force_rt.darrays[0].data)
if np.issubdtype(dtype, np.integer) or np.issubdtype(dtype, np.floating):
    compat_rt = img.from_bytes(img.to_bytes(mode='compat'))
    compat_darr = compat_rt.darrays[0].data
    assert np.allclose(cast, compat_darr)
    assert compat_darr.dtype in ('uint8', 'int32', 'float32')
else:
    with pytest.raises(ValueError):
        img.to_bytes(mode='compat')
if label in ('uint8', 'int32', 'float32'):
    strict_rt = img.from_bytes(img.to_bytes(mode='strict'))
    assert np.array_equal(cast, strict_rt.darrays[0].data)
else:
    with pytest.raises(ValueError):
        img.to_bytes(mode='strict')
```

## Next Steps


---

*Source: test_gifti.py:131 | Complexity: Advanced | Last updated: 2026-05-18*