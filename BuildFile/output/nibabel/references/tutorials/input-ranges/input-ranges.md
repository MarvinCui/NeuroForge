# How To: Input Ranges

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test input ranges

## Prerequisites

**Required Modules:**
- `itertools`
- `io`
- `platform`
- `numpy`
- `pytest`
- `numpy.testing`
- `arraywriters`
- `casting`
- `testing`
- `volumeutils`


## Step-by-Step Guide

### Step 1: Assign arr = np.arange(...)

```python
arr = np.arange(-500, 501, 10, dtype=np.float64)
```

**Verification:**
```python
assert np.all(abs_err <= max_err)
```

### Step 2: Assign bio = BytesIO(...)

```python
bio = BytesIO()
```

**Verification:**
```python
assert min(abs_err) == abs_err[arr == 0]
```

### Step 3: Assign working_type = value

```python
working_type = np.float32
```

### Step 4: Assign work_eps = value

```python
work_eps = np.finfo(working_type).eps
```

### Step 5: Assign aw = SlopeInterArrayWriter(...)

```python
aw = SlopeInterArrayWriter(arr, out_type)
```

### Step 6: Call aw.to_fileobj()

```python
aw.to_fileobj(bio)
```

### Step 7: Assign arr2 = array_from_file(...)

```python
arr2 = array_from_file(arr.shape, out_type, bio)
```

### Step 8: Assign arr3 = apply_read_scaling(...)

```python
arr3 = apply_read_scaling(arr2, aw.slope, aw.inter)
```

### Step 9: Assign max_miss = value

```python
max_miss = np.abs(aw.slope) / working_type(2.0) + work_eps * 10
```

### Step 10: Assign abs_err = np.abs(...)

```python
abs_err = np.abs(arr - arr3)
```

### Step 11: Assign max_err = value

```python
max_err = np.abs(arr) * work_eps + max_miss
```

**Verification:**
```python
assert np.all(abs_err <= max_err)
```

### Step 12: Call bio.truncate()

```python
bio.truncate(0)
```

### Step 13: Call bio.seek()

```python
bio.seek(0)
```

**Verification:**
```python
assert min(abs_err) == abs_err[arr == 0]
```


## Complete Example

```python
# Workflow
arr = np.arange(-500, 501, 10, dtype=np.float64)
bio = BytesIO()
working_type = np.float32
work_eps = np.finfo(working_type).eps
for out_type, offset in itertools.product(IUINT_TYPES, range(-1000, 1000, 100)):
    aw = SlopeInterArrayWriter(arr, out_type)
    aw.to_fileobj(bio)
    arr2 = array_from_file(arr.shape, out_type, bio)
    arr3 = apply_read_scaling(arr2, aw.slope, aw.inter)
    max_miss = np.abs(aw.slope) / working_type(2.0) + work_eps * 10
    abs_err = np.abs(arr - arr3)
    max_err = np.abs(arr) * work_eps + max_miss
    assert np.all(abs_err <= max_err)
    if out_type in UINT_TYPES and 0 in (min(arr), max(arr)):
        assert min(abs_err) == abs_err[arr == 0]
    bio.truncate(0)
    bio.seek(0)
```

## Next Steps


---

*Source: test_arraywriters.py:466 | Complexity: Advanced | Last updated: 2026-05-18*