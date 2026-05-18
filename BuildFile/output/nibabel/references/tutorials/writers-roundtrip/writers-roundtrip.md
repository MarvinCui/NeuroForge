# How To: Writers Roundtrip

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test writers roundtrip

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

### Step 1: Assign ndt = np.dtype(...)

```python
ndt = np.dtype(np.float64)
```

**Verification:**
```python
assert_array_equal(data_back, arr)
```

### Step 2: Assign arr = np.arange(...)

```python
arr = np.arange(3, dtype=ndt)
```

**Verification:**
```python
assert_array_equal(data_back, arr)
```

### Step 3: Assign aw = SlopeInterArrayWriter(...)

```python
aw = SlopeInterArrayWriter(arr, ndt, calc_scale=False)
```

**Verification:**
```python
assert_array_equal(data_back, np.zeros(arr.shape))
```

### Step 4: Assign aw.inter = 1.0

```python
aw.inter = 1.0
```

**Verification:**
```python
assert_array_almost_equal(data_back, [2, 1, 2])
```

### Step 5: Assign data_back = round_trip(...)

```python
data_back = round_trip(aw)
```

### Step 6: Call assert_array_equal()

```python
assert_array_equal(data_back, arr)
```

### Step 7: Assign aw.slope = 2.0

```python
aw.slope = 2.0
```

### Step 8: Assign data_back = round_trip(...)

```python
data_back = round_trip(aw)
```

### Step 9: Call assert_array_equal()

```python
assert_array_equal(data_back, arr)
```

### Step 10: Assign aw = SlopeInterArrayWriter(...)

```python
aw = SlopeInterArrayWriter(arr + np.nan, np.int32)
```

### Step 11: Assign data_back = round_trip(...)

```python
data_back = round_trip(aw)
```

### Step 12: Call assert_array_equal()

```python
assert_array_equal(data_back, np.zeros(arr.shape))
```

### Step 13: Assign unknown = value

```python
arr[0] = np.inf
```

### Step 14: Assign aw = SlopeInterArrayWriter(...)

```python
aw = SlopeInterArrayWriter(arr, np.int32)
```

### Step 15: Assign data_back = round_trip(...)

```python
data_back = round_trip(aw)
```

### Step 16: Call assert_array_almost_equal()

```python
assert_array_almost_equal(data_back, [2, 1, 2])
```


## Complete Example

```python
# Workflow
ndt = np.dtype(np.float64)
arr = np.arange(3, dtype=ndt)
aw = SlopeInterArrayWriter(arr, ndt, calc_scale=False)
aw.inter = 1.0
data_back = round_trip(aw)
assert_array_equal(data_back, arr)
aw.slope = 2.0
data_back = round_trip(aw)
assert_array_equal(data_back, arr)
aw = SlopeInterArrayWriter(arr + np.nan, np.int32)
data_back = round_trip(aw)
assert_array_equal(data_back, np.zeros(arr.shape))
arr[0] = np.inf
aw = SlopeInterArrayWriter(arr, np.int32)
data_back = round_trip(aw)
assert_array_almost_equal(data_back, [2, 1, 2])
```

## Next Steps


---

*Source: test_arraywriters.py:534 | Complexity: Advanced | Last updated: 2026-05-18*