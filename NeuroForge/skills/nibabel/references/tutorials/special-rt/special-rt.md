# How To: Special Rt

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test special rt

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

### Step 1: Assign arr = np.array(...)

```python
arr = np.array([np.inf, np.nan, -np.inf])
```

**Verification:**
```python
assert np.allclose(round_trip(aw).astype(float), [mx, 0, mn])
```

### Step 2: Assign arr = np.zeros(...)

```python
arr = np.zeros((3,), dtype=in_dtt)
```

**Verification:**
```python
assert get_slope_inter(aw) == (1, 0)
```

### Step 3: Assign aw = awt(...)

```python
aw = awt(arr, out_dtt)
```

**Verification:**
```python
assert_array_equal(round_trip(aw), 0)
```

### Step 4: Call assert_array_equal()

```python
assert_array_equal(round_trip(aw), 0)
```

**Verification:**
```python
assert get_slope_inter(aw) == (1, 0)
```

### Step 5: Assign in_arr = arr.astype(...)

```python
in_arr = arr.astype(in_dtt)
```

**Verification:**
```python
assert_array_equal(round_trip(aw), 0)
```

### Step 6: Assign aw = ArrayWriter(...)

```python
aw = ArrayWriter(in_arr, out_dtt, check_scaling=False)
```

### Step 7: Assign unknown = shared_range(...)

```python
mn, mx = shared_range(float, out_dtt)
```

**Verification:**
```python
assert np.allclose(round_trip(aw).astype(float), [mx, 0, mn])
```

### Step 8: Call ArrayWriter()

```python
ArrayWriter(in_arr, out_dtt)
```

### Step 9: Assign aw = klass(...)

```python
aw = klass(in_arr, out_dtt)
```

**Verification:**
```python
assert get_slope_inter(aw) == (1, 0)
```

### Step 10: Call assert_array_equal()

```python
assert_array_equal(round_trip(aw), 0)
```


## Complete Example

```python
# Workflow
arr = np.array([np.inf, np.nan, -np.inf])
for in_dtt in FLOAT_TYPES:
    for out_dtt in IUINT_TYPES:
        in_arr = arr.astype(in_dtt)
        with pytest.raises(WriterError):
            ArrayWriter(in_arr, out_dtt)
        aw = ArrayWriter(in_arr, out_dtt, check_scaling=False)
        mn, mx = shared_range(float, out_dtt)
        assert np.allclose(round_trip(aw).astype(float), [mx, 0, mn])
        for klass in (SlopeArrayWriter, SlopeInterArrayWriter):
            aw = klass(in_arr, out_dtt)
            assert get_slope_inter(aw) == (1, 0)
            assert_array_equal(round_trip(aw), 0)
for in_dtt, out_dtt, awt in itertools.product(FLOAT_TYPES, IUINT_TYPES, (ArrayWriter, SlopeArrayWriter, SlopeInterArrayWriter)):
    arr = np.zeros((3,), dtype=in_dtt)
    aw = awt(arr, out_dtt)
    assert get_slope_inter(aw) == (1, 0)
    assert_array_equal(round_trip(aw), 0)
```

## Next Steps


---

*Source: test_arraywriters.py:236 | Complexity: Advanced | Last updated: 2026-05-18*