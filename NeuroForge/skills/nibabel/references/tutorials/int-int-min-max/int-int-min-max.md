# How To: Int Int Min Max

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test int int min max

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

### Step 1: Assign eps = value

```python
eps = np.finfo(np.float64).eps
```

**Verification:**
```python
assert np.all(rdiff < rtol)
```

### Step 2: Assign rtol = 1e-06

```python
rtol = 1e-06
```

### Step 3: Assign iinf = np.iinfo(...)

```python
iinf = np.iinfo(in_dt)
```

### Step 4: Assign arr = np.array(...)

```python
arr = np.array([iinf.min, iinf.max], dtype=in_dt)
```

### Step 5: Assign arr_back_sc = round_trip(...)

```python
arr_back_sc = round_trip(aw)
```

### Step 6: Assign adiff = int_abs(...)

```python
adiff = int_abs(arr - arr_back_sc)
```

### Step 7: Assign rdiff = value

```python
rdiff = adiff / (arr + eps)
```

**Verification:**
```python
assert np.all(rdiff < rtol)
```

### Step 8: Assign aw = SlopeInterArrayWriter(...)

```python
aw = SlopeInterArrayWriter(arr, out_dt)
```


## Complete Example

```python
# Workflow
eps = np.finfo(np.float64).eps
rtol = 1e-06
for in_dt in IUINT_TYPES:
    iinf = np.iinfo(in_dt)
    arr = np.array([iinf.min, iinf.max], dtype=in_dt)
    for out_dt in IUINT_TYPES:
        try:
            aw = SlopeInterArrayWriter(arr, out_dt)
        except ScalingError:
            continue
        arr_back_sc = round_trip(aw)
        adiff = int_abs(arr - arr_back_sc)
        rdiff = adiff / (arr + eps)
        assert np.all(rdiff < rtol)
```

## Next Steps


---

*Source: test_arraywriters.py:647 | Complexity: Advanced | Last updated: 2026-05-18*