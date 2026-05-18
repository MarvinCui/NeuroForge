# How To: Array File Scales

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test array file scales

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `warnings`
- `io`
- `numpy`
- `pytest`
- `numpy.testing`
- `casting`
- `testing`
- `volumeutils`
- `test_volumeutils`

**Setup Required:**
```python
# Fixtures: in_type, out_type
```

## Step-by-Step Guide

### Step 1: Assign bio = BytesIO(...)

```python
bio = BytesIO()
```

**Verification:**
```python
assert np.all(np.abs(arr - arr3) <= max_miss)
```

### Step 2: Assign out_dtype = np.dtype(...)

```python
out_dtype = np.dtype(out_type)
```

### Step 3: Assign arr = np.zeros(...)

```python
arr = np.zeros((3,), dtype=in_type)
```

### Step 4: Assign info = type_info(...)

```python
info = type_info(in_type)
```

### Step 5: Assign unknown = value

```python
arr[0], arr[1] = (info['min'], info['max'])
```

### Step 6: Assign unknown = _calculate_scale(...)

```python
slope, inter, mn, mx = _calculate_scale(arr, out_dtype, True)
```

### Step 7: Call array_to_file()

```python
array_to_file(arr, bio, out_type, 0, inter, slope, mn, mx)
```

### Step 8: Call bio.seek()

```python
bio.seek(0)
```

### Step 9: Assign arr2 = array_from_file(...)

```python
arr2 = array_from_file(arr.shape, out_dtype, bio)
```

### Step 10: Assign arr3 = apply_read_scaling(...)

```python
arr3 = apply_read_scaling(arr2, slope, inter)
```

### Step 11: Assign max_miss = value

```python
max_miss = slope / 2.0
```

**Verification:**
```python
assert np.all(np.abs(arr - arr3) <= max_miss)
```


## Complete Example

```python
# Setup
# Fixtures: in_type, out_type

# Workflow
bio = BytesIO()
out_dtype = np.dtype(out_type)
arr = np.zeros((3,), dtype=in_type)
info = type_info(in_type)
arr[0], arr[1] = (info['min'], info['max'])
slope, inter, mn, mx = _calculate_scale(arr, out_dtype, True)
array_to_file(arr, bio, out_type, 0, inter, slope, mn, mx)
bio.seek(0)
arr2 = array_from_file(arr.shape, out_dtype, bio)
arr3 = apply_read_scaling(arr2, slope, inter)
max_miss = slope / 2.0
assert np.all(np.abs(arr - arr3) <= max_miss)
```

## Next Steps


---

*Source: test_scaling.py:146 | Complexity: Advanced | Last updated: 2026-05-18*