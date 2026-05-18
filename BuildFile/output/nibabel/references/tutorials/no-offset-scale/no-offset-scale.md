# How To: No Offset Scale

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test no offset scale

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

### Step 1: Assign SAW = SlopeArrayWriter

```python
SAW = SlopeArrayWriter
```

**Verification:**
```python
assert aw.slope == 1.0
```

### Step 2: Assign aw = SAW(...)

```python
aw = SAW(np.array([-126, 127 * 2.0], dtype=np.float32), np.int8)
```

**Verification:**
```python
assert aw.slope == 2
```

### Step 3: Assign aw = SAW(...)

```python
aw = SAW(np.array([-128 * 2.0, 127], dtype=np.float32), np.int8)
```

**Verification:**
```python
assert aw.slope == 2
```

### Step 4: Assign n = value

```python
n = -2 ** 15
```

**Verification:**
```python
assert_array_almost_equal(aw.slope, n / 255.0, 5)
```

### Step 5: Assign aw = SAW(...)

```python
aw = SAW(np.array([n, n], dtype=np.int16), np.uint8)
```

### Step 6: Call assert_array_almost_equal()

```python
assert_array_almost_equal(aw.slope, n / 255.0, 5)
```

### Step 7: Assign aw = SAW(...)

```python
aw = SAW(np.array(data, dtype=np.float32), np.int8)
```

**Verification:**
```python
assert aw.slope == 1.0
```


## Complete Example

```python
# Workflow
SAW = SlopeArrayWriter
for data in ((-128, 127), (-128, 126), (-128, -127), (-128, 0), (-128, -1), (126, 127), (-127, 127)):
    aw = SAW(np.array(data, dtype=np.float32), np.int8)
    assert aw.slope == 1.0
aw = SAW(np.array([-126, 127 * 2.0], dtype=np.float32), np.int8)
assert aw.slope == 2
aw = SAW(np.array([-128 * 2.0, 127], dtype=np.float32), np.int8)
assert aw.slope == 2
n = -2 ** 15
aw = SAW(np.array([n, n], dtype=np.int16), np.uint8)
assert_array_almost_equal(aw.slope, n / 255.0, 5)
```

## Next Steps


---

*Source: test_arraywriters.py:390 | Complexity: Intermediate | Last updated: 2026-05-18*