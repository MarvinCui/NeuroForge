# How To: With Offset Scale

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test with offset scale

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

### Step 1: Assign SIAW = SlopeInterArrayWriter

```python
SIAW = SlopeInterArrayWriter
```

**Verification:**
```python
assert (aw.slope, aw.inter) == (1, 0)
```

### Step 2: Assign aw = SIAW(...)

```python
aw = SIAW(np.array([0, 127], dtype=np.int8), np.uint8)
```

**Verification:**
```python
assert (aw.slope, aw.inter) == (1, -1)
```

### Step 3: Assign aw = SIAW(...)

```python
aw = SIAW(np.array([-1, 126], dtype=np.int8), np.uint8)
```

**Verification:**
```python
assert (aw.slope, aw.inter) == (1, -1)
```

### Step 4: Assign aw = SIAW(...)

```python
aw = SIAW(np.array([-1, 254], dtype=np.int16), np.uint8)
```

**Verification:**
```python
assert (aw.slope, aw.inter) != (1, -1)
```

### Step 5: Assign aw = SIAW(...)

```python
aw = SIAW(np.array([-1, 255], dtype=np.int16), np.uint8)
```

**Verification:**
```python
assert (aw.slope, aw.inter) == (1, -256)
```

### Step 6: Assign aw = SIAW(...)

```python
aw = SIAW(np.array([-256, -2], dtype=np.int16), np.uint8)
```

**Verification:**
```python
assert (aw.slope, aw.inter) == (1, -129)
```

### Step 7: Assign aw = SIAW(...)

```python
aw = SIAW(np.array([-256, -2], dtype=np.int16), np.int8)
```

**Verification:**
```python
assert (aw.slope, aw.inter) == (1, -129)
```


## Complete Example

```python
# Workflow
SIAW = SlopeInterArrayWriter
aw = SIAW(np.array([0, 127], dtype=np.int8), np.uint8)
assert (aw.slope, aw.inter) == (1, 0)
aw = SIAW(np.array([-1, 126], dtype=np.int8), np.uint8)
assert (aw.slope, aw.inter) == (1, -1)
aw = SIAW(np.array([-1, 254], dtype=np.int16), np.uint8)
assert (aw.slope, aw.inter) == (1, -1)
aw = SIAW(np.array([-1, 255], dtype=np.int16), np.uint8)
assert (aw.slope, aw.inter) != (1, -1)
aw = SIAW(np.array([-256, -2], dtype=np.int16), np.uint8)
assert (aw.slope, aw.inter) == (1, -256)
aw = SIAW(np.array([-256, -2], dtype=np.int16), np.int8)
assert (aw.slope, aw.inter) == (1, -129)
```

## Next Steps


---

*Source: test_arraywriters.py:415 | Complexity: Intermediate | Last updated: 2026-05-18*