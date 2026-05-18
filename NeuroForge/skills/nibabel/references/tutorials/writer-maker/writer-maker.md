# How To: Writer Maker

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test writer maker

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
arr = np.arange(10, dtype=np.float64)
```

**Verification:**
```python
assert isinstance(aw, SlopeInterArrayWriter)
```

### Step 2: Assign aw = make_array_writer(...)

```python
aw = make_array_writer(arr, np.float64)
```

**Verification:**
```python
assert isinstance(aw, SlopeInterArrayWriter)
```

### Step 3: Assign aw = make_array_writer(...)

```python
aw = make_array_writer(arr, np.float64, True, True)
```

**Verification:**
```python
assert isinstance(aw, SlopeArrayWriter)
```

### Step 4: Assign aw = make_array_writer(...)

```python
aw = make_array_writer(arr, np.float64, True, False)
```

**Verification:**
```python
assert isinstance(aw, ArrayWriter)
```

### Step 5: Assign aw = make_array_writer(...)

```python
aw = make_array_writer(arr, np.float64, False, False)
```

**Verification:**
```python
assert (aw.slope, aw.inter) == (1, 0)
```

### Step 6: Assign aw = make_array_writer(...)

```python
aw = make_array_writer(arr, np.int16, calc_scale=False)
```

**Verification:**
```python
assert not (slope, inter) == (1, 0)
```

### Step 7: Call aw.calc_scale()

```python
aw.calc_scale()
```

**Verification:**
```python
assert (aw.slope, aw.inter) == (slope, inter)
```

### Step 8: Assign unknown = value

```python
slope, inter = (aw.slope, aw.inter)
```

**Verification:**
```python
assert (aw.slope, aw.inter) == (slope, inter)
```

### Step 9: Assign aw = make_array_writer(...)

```python
aw = make_array_writer(arr, np.int16)
```

**Verification:**
```python
assert (aw.slope, aw.inter) == (slope, inter)
```

### Step 10: Assign aw = make_array_writer(...)

```python
aw = make_array_writer(arr, np.int16, calc_scale=True)
```

**Verification:**
```python
assert (aw.slope, aw.inter) == (slope, inter)
```

### Step 11: Call make_array_writer()

```python
make_array_writer(arr, np.float64, False)
```

### Step 12: Call make_array_writer()

```python
make_array_writer(arr, np.float64, False, True)
```


## Complete Example

```python
# Workflow
arr = np.arange(10, dtype=np.float64)
aw = make_array_writer(arr, np.float64)
assert isinstance(aw, SlopeInterArrayWriter)
aw = make_array_writer(arr, np.float64, True, True)
assert isinstance(aw, SlopeInterArrayWriter)
aw = make_array_writer(arr, np.float64, True, False)
assert isinstance(aw, SlopeArrayWriter)
aw = make_array_writer(arr, np.float64, False, False)
assert isinstance(aw, ArrayWriter)
with pytest.raises(ValueError):
    make_array_writer(arr, np.float64, False)
with pytest.raises(ValueError):
    make_array_writer(arr, np.float64, False, True)
aw = make_array_writer(arr, np.int16, calc_scale=False)
assert (aw.slope, aw.inter) == (1, 0)
aw.calc_scale()
slope, inter = (aw.slope, aw.inter)
assert not (slope, inter) == (1, 0)
aw = make_array_writer(arr, np.int16)
assert (aw.slope, aw.inter) == (slope, inter)
aw = make_array_writer(arr, np.int16, calc_scale=True)
assert (aw.slope, aw.inter) == (slope, inter)
```

## Next Steps


---

*Source: test_arraywriters.py:601 | Complexity: Advanced | Last updated: 2026-05-18*