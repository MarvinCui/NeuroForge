# How To: Gridindices

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test GridIndices

## Prerequisites

**Required Modules:**
- `math`
- `pathlib`
- `numpy`
- `pytest`
- `nibabel`
- `nibabel.affines`
- `nibabel.fileslice`
- `nibabel.optpkg`
- `nibabel.spatialimages`
- `nibabel.tests.nibabel_data`


## Step-by-Step Guide

### Step 1: Assign shape = value

```python
shape = (2, 3)
```

**Verification:**
```python
assert gi.dtype == np.dtype('u1')
```

### Step 2: Assign gi = ps.GridIndices(...)

```python
gi = ps.GridIndices(shape)
```

**Verification:**
```python
assert gi.shape == (6, 2)
```

### Step 3: Assign gi_arr = np.asanyarray(...)

```python
gi_arr = np.asanyarray(gi)
```

**Verification:**
```python
assert repr(gi) == '<GridIndices(2, 3)>'
```

### Step 4: Assign shape = value

```python
shape = (2, 3, 4)
```

**Verification:**
```python
assert gi_arr.dtype == np.dtype('u1')
```

### Step 5: Assign gi = ps.GridIndices(...)

```python
gi = ps.GridIndices(shape)
```

**Verification:**
```python
assert gi_arr.shape == (6, 2)
```

### Step 6: Assign gi_arr = np.asanyarray(...)

```python
gi_arr = np.asanyarray(gi)
```

**Verification:**
```python
assert np.array_equal(gi_arr, [[0, 0], [0, 1], [0, 2], [1, 0], [1, 1], [1, 2]])
```


## Complete Example

```python
# Workflow
shape = (2, 3)
gi = ps.GridIndices(shape)
assert gi.dtype == np.dtype('u1')
assert gi.shape == (6, 2)
assert repr(gi) == '<GridIndices(2, 3)>'
gi_arr = np.asanyarray(gi)
assert gi_arr.dtype == np.dtype('u1')
assert gi_arr.shape == (6, 2)
assert np.array_equal(gi_arr, [[0, 0], [0, 1], [0, 2], [1, 0], [1, 1], [1, 2]])
shape = (2, 3, 4)
gi = ps.GridIndices(shape)
assert gi.dtype == np.dtype('u1')
assert gi.shape == (24, 3)
assert repr(gi) == '<GridIndices(2, 3, 4)>'
gi_arr = np.asanyarray(gi)
assert gi_arr.dtype == np.dtype('u1')
assert gi_arr.shape == (24, 3)
assert np.array_equal(gi_arr, np.mgrid[:2, :3, :4].reshape(3, -1).T)
```

## Next Steps


---

*Source: test_pointset.py:102 | Complexity: Intermediate | Last updated: 2026-05-18*