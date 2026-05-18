# How To: Finite Range

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test finite range

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
# Fixtures: in_arr, res
```

## Step-by-Step Guide

### Step 1: Assign has_nan = np.any(...)

```python
has_nan = np.any(np.isnan(in_arr))
```

**Verification:**
```python
assert finite_range(in_arr) == res
```

### Step 2: Assign in_arr = np.array(...)

```python
in_arr = np.array(in_arr)
```

**Verification:**
```python
assert finite_range(in_arr, False) == res
```

### Step 3: Assign flat_arr = in_arr.ravel(...)

```python
flat_arr = in_arr.ravel()
```

**Verification:**
```python
assert finite_range(in_arr, check_nan=False) == res
```

### Step 4: Assign c_arr = in_arr.astype(...)

```python
c_arr = in_arr.astype(np.complex128)
```

**Verification:**
```python
assert finite_range(in_arr, True) == res + (has_nan,)
```


## Complete Example

```python
# Setup
# Fixtures: in_arr, res

# Workflow
assert finite_range(in_arr) == res
assert finite_range(in_arr, False) == res
assert finite_range(in_arr, check_nan=False) == res
has_nan = np.any(np.isnan(in_arr))
assert finite_range(in_arr, True) == res + (has_nan,)
assert finite_range(in_arr, check_nan=True) == res + (has_nan,)
in_arr = np.array(in_arr)
flat_arr = in_arr.ravel()
assert finite_range(flat_arr) == res
assert finite_range(flat_arr, True) == res + (has_nan,)
if in_arr.dtype.kind == 'f':
    c_arr = in_arr.astype(np.complex128)
    assert finite_range(c_arr) == res
    assert finite_range(c_arr, True) == res + (has_nan,)
```

## Next Steps


---

*Source: test_scaling.py:53 | Complexity: Intermediate | Last updated: 2026-05-18*