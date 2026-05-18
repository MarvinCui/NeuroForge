# How To: Shapes

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test shapes

## Prerequisites

**Required Modules:**
- `itertools`
- `logging`
- `os`
- `pickle`
- `re`
- `io`
- `numpy`
- `pytest`
- `numpy.testing`
- `_compression`
- `analyze`
- `arraywriters`
- `casting`
- `nifti1`
- `spatialimages`
- `testing`
- `tmpdirs`


## Step-by-Step Guide

### Step 1: Assign hdr = self.header_class(...)

```python
hdr = self.header_class()
```

**Verification:**
```python
assert hdr.get_data_shape() == shape
```

### Step 2: Assign dim_dtype = value

```python
dim_dtype = hdr.structarr['dim'].dtype
```

**Verification:**
```python
assert hdr.get_data_shape() == shape
```

### Step 3: Assign mx = int(...)

```python
mx = int(np.iinfo(dim_dtype).max)
```

**Verification:**
```python
assert hdr.get_data_shape() == shape
```

### Step 4: Assign shape = value

```python
shape = (mx,)
```

### Step 5: Call hdr.set_data_shape()

```python
hdr.set_data_shape(shape)
```

**Verification:**
```python
assert hdr.get_data_shape() == shape
```

### Step 6: Assign shape = value

```python
shape = (mx + 1,)
```

### Step 7: Assign shape = value

```python
shape = (2, 3, 4)
```

### Step 8: Call hdr.set_data_shape()

```python
hdr.set_data_shape(shape)
```

**Verification:**
```python
assert hdr.get_data_shape() == shape
```

### Step 9: Call hdr.set_data_shape()

```python
hdr.set_data_shape(shape)
```

### Step 10: Call hdr.set_data_shape()

```python
hdr.set_data_shape(constructor(shape))
```

**Verification:**
```python
assert hdr.get_data_shape() == shape
```


## Complete Example

```python
# Workflow
hdr = self.header_class()
for shape in ((2, 3, 4), (2, 3, 4, 5), (2, 3), (2,)):
    hdr.set_data_shape(shape)
    assert hdr.get_data_shape() == shape
dim_dtype = hdr.structarr['dim'].dtype
mx = int(np.iinfo(dim_dtype).max)
shape = (mx,)
hdr.set_data_shape(shape)
assert hdr.get_data_shape() == shape
shape = (mx + 1,)
with pytest.raises(HeaderDataError):
    hdr.set_data_shape(shape)
shape = (2, 3, 4)
for constructor in (list, tuple, np.array):
    hdr.set_data_shape(constructor(shape))
    assert hdr.get_data_shape() == shape
```

## Next Steps


---

*Source: test_analyze.py:304 | Complexity: Advanced | Last updated: 2026-05-18*