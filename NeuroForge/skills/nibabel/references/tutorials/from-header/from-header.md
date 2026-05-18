# How To: From Header

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test from header

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

### Step 1: Assign empty = SpatialHeader.from_header(...)

```python
empty = SpatialHeader.from_header()
```

**Verification:**
```python
assert SpatialHeader() == empty
```

### Step 2: Assign empty = SpatialHeader.from_header(...)

```python
empty = SpatialHeader.from_header(None)
```

**Verification:**
```python
assert SpatialHeader() == empty
```

### Step 3: Assign hdr = SpatialHeader(...)

```python
hdr = SpatialHeader(np.float64, shape=(1, 2, 3), zooms=(3.0, 2.0, 1.0))
```

**Verification:**
```python
assert hdr == copy
```

### Step 4: Assign copy = SpatialHeader.from_header(...)

```python
copy = SpatialHeader.from_header(hdr)
```

**Verification:**
```python
assert hdr is not copy
```

### Step 5: Assign converted = SpatialHeader.from_header(...)

```python
converted = SpatialHeader.from_header(C())
```

**Verification:**
```python
assert isinstance(converted, SpatialHeader)
```


## Complete Example

```python
# Workflow
empty = SpatialHeader.from_header()
assert SpatialHeader() == empty
empty = SpatialHeader.from_header(None)
assert SpatialHeader() == empty
hdr = SpatialHeader(np.float64, shape=(1, 2, 3), zooms=(3.0, 2.0, 1.0))
copy = SpatialHeader.from_header(hdr)
assert hdr == copy
assert hdr is not copy

class C:

    def get_data_dtype(self):
        return np.dtype('u2')

    def get_data_shape(self):
        return (5, 4, 3)

    def get_zooms(self):
        return (10.0, 9.0, 8.0)
converted = SpatialHeader.from_header(C())
assert isinstance(converted, SpatialHeader)
assert converted.get_data_dtype() == np.dtype('u2')
assert converted.get_data_shape() == (5, 4, 3)
assert converted.get_zooms() == (10.0, 9.0, 8.0)
```

## Next Steps


---

*Source: test_spatialimages.py:48 | Complexity: Intermediate | Last updated: 2026-05-18*