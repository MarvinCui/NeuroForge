# How To: Header Init

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test header init

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

### Step 1: Assign hdr = SpatialHeader(...)

```python
hdr = SpatialHeader()
```

**Verification:**
```python
assert hdr.get_data_dtype() == np.dtype(np.float32)
```

### Step 2: Assign hdr = SpatialHeader(...)

```python
hdr = SpatialHeader(np.float64)
```

**Verification:**
```python
assert hdr.get_data_shape() == (0,)
```

### Step 3: Assign hdr = SpatialHeader(...)

```python
hdr = SpatialHeader(np.float64, shape=(1, 2, 3))
```

**Verification:**
```python
assert hdr.get_zooms() == (1.0,)
```

### Step 4: Assign hdr = SpatialHeader(...)

```python
hdr = SpatialHeader(np.float64, shape=(1, 2, 3), zooms=None)
```

**Verification:**
```python
assert hdr.get_data_dtype() == np.dtype(np.float64)
```

### Step 5: Assign hdr = SpatialHeader(...)

```python
hdr = SpatialHeader(np.float64, shape=(1, 2, 3), zooms=(3.0, 2.0, 1.0))
```

**Verification:**
```python
assert hdr.get_data_shape() == (0,)
```


## Complete Example

```python
# Workflow
hdr = SpatialHeader()
assert hdr.get_data_dtype() == np.dtype(np.float32)
assert hdr.get_data_shape() == (0,)
assert hdr.get_zooms() == (1.0,)
hdr = SpatialHeader(np.float64)
assert hdr.get_data_dtype() == np.dtype(np.float64)
assert hdr.get_data_shape() == (0,)
assert hdr.get_zooms() == (1.0,)
hdr = SpatialHeader(np.float64, shape=(1, 2, 3))
assert hdr.get_data_dtype() == np.dtype(np.float64)
assert hdr.get_data_shape() == (1, 2, 3)
assert hdr.get_zooms() == (1.0, 1.0, 1.0)
hdr = SpatialHeader(np.float64, shape=(1, 2, 3), zooms=None)
assert hdr.get_data_dtype() == np.dtype(np.float64)
assert hdr.get_data_shape() == (1, 2, 3)
assert hdr.get_zooms() == (1.0, 1.0, 1.0)
hdr = SpatialHeader(np.float64, shape=(1, 2, 3), zooms=(3.0, 2.0, 1.0))
assert hdr.get_data_dtype() == np.dtype(np.float64)
assert hdr.get_data_shape() == (1, 2, 3)
assert hdr.get_zooms() == (3.0, 2.0, 1.0)
```

## Next Steps


---

*Source: test_spatialimages.py:24 | Complexity: Intermediate | Last updated: 2026-05-18*