# How To: Calculate Scale

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test calculate scale

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

### Step 1: Assign npa = value

```python
npa = np.array
```

**Verification:**
```python
assert get_slope_inter(aw) == (1.0, -2.0)
```

### Step 2: Assign SIAW = SlopeInterArrayWriter

```python
SIAW = SlopeInterArrayWriter
```

**Verification:**
```python
assert get_slope_inter(aw) == (-1.0, 0.0)
```

### Step 3: Assign SAW = SlopeArrayWriter

```python
SAW = SlopeArrayWriter
```

**Verification:**
```python
assert get_slope_inter(aw) == (-1.0, 0.0)
```

### Step 4: Assign aw = SIAW(...)

```python
aw = SIAW(npa([-2, -1], dtype=np.int8), np.uint8)
```

**Verification:**
```python
assert get_slope_inter(aw) == (-2.0, 0.0)
```

### Step 5: Assign aw = SAW(...)

```python
aw = SAW(npa([-2, -1], dtype=np.int8), np.uint8)
```

**Verification:**
```python
assert get_slope_inter(aw) != (-1.0, 0.0)
```

### Step 6: Assign aw = SAW(...)

```python
aw = SAW(npa([-2, 0], dtype=np.int8), np.uint8)
```

**Verification:**
```python
assert get_slope_inter(aw) == (1.0, -1.0)
```

### Step 7: Assign aw = SAW(...)

```python
aw = SAW(npa([-510, 0], dtype=np.int16), np.uint8)
```

**Verification:**
```python
assert slope_inter != (1.0, -1.0)
```

### Step 8: Assign aw = SAW(...)

```python
aw = SAW(npa([-2, 0], dtype=np.float32), np.uint8)
```

**Verification:**
```python
assert get_slope_inter(aw) != (-1.0, 0.0)
```

### Step 9: Assign aw = SIAW(...)

```python
aw = SIAW(npa([-1, 1], dtype=np.int8), np.uint8)
```

**Verification:**
```python
assert get_slope_inter(aw) == (1.0, -1.0)
```

### Step 10: Assign aw = SIAW(...)

```python
aw = SIAW(npa([-1, 255], dtype=np.int16), np.uint8)
```

### Step 11: Assign slope_inter = get_slope_inter(...)

```python
slope_inter = get_slope_inter(aw)
```

**Verification:**
```python
assert slope_inter != (1.0, -1.0)
```

### Step 12: Call SAW()

```python
SAW(npa([-1, 1], dtype=np.int8), np.uint8)
```


## Complete Example

```python
# Workflow
npa = np.array
SIAW = SlopeInterArrayWriter
SAW = SlopeArrayWriter
aw = SIAW(npa([-2, -1], dtype=np.int8), np.uint8)
assert get_slope_inter(aw) == (1.0, -2.0)
aw = SAW(npa([-2, -1], dtype=np.int8), np.uint8)
assert get_slope_inter(aw) == (-1.0, 0.0)
aw = SAW(npa([-2, 0], dtype=np.int8), np.uint8)
assert get_slope_inter(aw) == (-1.0, 0.0)
aw = SAW(npa([-510, 0], dtype=np.int16), np.uint8)
assert get_slope_inter(aw) == (-2.0, 0.0)
aw = SAW(npa([-2, 0], dtype=np.float32), np.uint8)
assert get_slope_inter(aw) != (-1.0, 0.0)
aw = SIAW(npa([-1, 1], dtype=np.int8), np.uint8)
assert get_slope_inter(aw) == (1.0, -1.0)
with pytest.raises(WriterError):
    SAW(npa([-1, 1], dtype=np.int8), np.uint8)
aw = SIAW(npa([-1, 255], dtype=np.int16), np.uint8)
slope_inter = get_slope_inter(aw)
assert slope_inter != (1.0, -1.0)
```

## Next Steps


---

*Source: test_arraywriters.py:334 | Complexity: Advanced | Last updated: 2026-05-18*