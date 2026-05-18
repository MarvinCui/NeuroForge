# How To: Eq

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test eq

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
assert hdr == other
```

### Step 2: Assign other = SpatialHeader(...)

```python
other = SpatialHeader()
```

**Verification:**
```python
assert hdr != other
```

### Step 3: Assign other = SpatialHeader(...)

```python
other = SpatialHeader('u2')
```

**Verification:**
```python
assert hdr != other
```

### Step 4: Assign other = SpatialHeader(...)

```python
other = SpatialHeader(shape=(1, 2, 3))
```

**Verification:**
```python
assert hdr == other
```

### Step 5: Assign hdr = SpatialHeader(...)

```python
hdr = SpatialHeader(shape=(1, 2))
```

**Verification:**
```python
assert hdr != other
```

### Step 6: Assign other = SpatialHeader(...)

```python
other = SpatialHeader(shape=(1, 2))
```

**Verification:**
```python
assert hdr == other
```

### Step 7: Assign other = SpatialHeader(...)

```python
other = SpatialHeader(shape=(1, 2), zooms=(2.0, 3.0))
```

**Verification:**
```python
assert hdr != other
```


## Complete Example

```python
# Workflow
hdr = SpatialHeader()
other = SpatialHeader()
assert hdr == other
other = SpatialHeader('u2')
assert hdr != other
other = SpatialHeader(shape=(1, 2, 3))
assert hdr != other
hdr = SpatialHeader(shape=(1, 2))
other = SpatialHeader(shape=(1, 2))
assert hdr == other
other = SpatialHeader(shape=(1, 2), zooms=(2.0, 3.0))
assert hdr != other
```

## Next Steps


---

*Source: test_spatialimages.py:77 | Complexity: Intermediate | Last updated: 2026-05-18*