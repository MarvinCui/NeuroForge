# How To: Bounding Box

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test bounding box

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `pytest`
- `scipy.ndimage`
- `dipy.data`
- `dipy.io.image`
- `dipy.segment.mask`
- `dipy.utils.deprecator`


## Step-by-Step Guide

### Step 1: Assign vol = np.zeros(...)

```python
vol = np.zeros((100, 100, 50), dtype=int)
```

**Verification:**
```python
assert_equal(mins, [10, 11, 5])
```

### Step 2: Assign unknown = 3

```python
vol[10:90, 11:40, 5:33] = 3
```

**Verification:**
```python
assert_equal(maxs, [90, 40, 33])
```

### Step 3: Assign unknown = bounding_box(...)

```python
mins, maxs = bounding_box(vol)
```

**Verification:**
```python
assert_equal(mins, [11, 5])
```

### Step 4: Call assert_equal()

```python
assert_equal(mins, [10, 11, 5])
```

**Verification:**
```python
assert_equal(maxs, [40, 33])
```

### Step 5: Call assert_equal()

```python
assert_equal(maxs, [90, 40, 33])
```

**Verification:**
```python
assert_equal(len(w), num_warns + 1)
```

### Step 6: Assign unknown = bounding_box(...)

```python
mins, maxs = bounding_box(vol[10])
```

**Verification:**
```python
assert_equal(mins, [0, 0, 0])
```

### Step 7: Call assert_equal()

```python
assert_equal(mins, [11, 5])
```

**Verification:**
```python
assert_equal(maxs, [0, 0, 0])
```

### Step 8: Call assert_equal()

```python
assert_equal(maxs, [40, 33])
```

**Verification:**
```python
assert_equal(len(w), num_warns + 2)
```

### Step 9: Assign unknown = 0

```python
vol[:] = 0
```

**Verification:**
```python
assert_equal(mins, [0, 0])
```

### Step 10: Call warnings.simplefilter()

```python
warnings.simplefilter('always')
```

**Verification:**
```python
assert_equal(maxs, [0, 0])
```

### Step 11: Assign num_warns = len(...)

```python
num_warns = len(w)
```

### Step 12: Assign unknown = bounding_box(...)

```python
mins, maxs = bounding_box(vol)
```

### Step 13: Call assert_equal()

```python
assert_equal(len(w), num_warns + 1)
```

### Step 14: Call assert_equal()

```python
assert_equal(mins, [0, 0, 0])
```

### Step 15: Call assert_equal()

```python
assert_equal(maxs, [0, 0, 0])
```

### Step 16: Assign unknown = bounding_box(...)

```python
mins, maxs = bounding_box(vol[0])
```

### Step 17: Call assert_equal()

```python
assert_equal(len(w), num_warns + 2)
```

### Step 18: Call assert_equal()

```python
assert_equal(mins, [0, 0])
```

### Step 19: Call assert_equal()

```python
assert_equal(maxs, [0, 0])
```


## Complete Example

```python
# Workflow
vol = np.zeros((100, 100, 50), dtype=int)
vol[10:90, 11:40, 5:33] = 3
mins, maxs = bounding_box(vol)
assert_equal(mins, [10, 11, 5])
assert_equal(maxs, [90, 40, 33])
mins, maxs = bounding_box(vol[10])
assert_equal(mins, [11, 5])
assert_equal(maxs, [40, 33])
vol[:] = 0
with warnings.catch_warnings(record=True) as w:
    warnings.simplefilter('always')
    num_warns = len(w)
    mins, maxs = bounding_box(vol)
    assert_equal(len(w), num_warns + 1)
    assert_equal(mins, [0, 0, 0])
    assert_equal(maxs, [0, 0, 0])
    mins, maxs = bounding_box(vol[0])
    assert_equal(len(w), num_warns + 2)
    assert_equal(mins, [0, 0])
    assert_equal(maxs, [0, 0])
```

## Next Steps


---

*Source: test_mask.py:56 | Complexity: Advanced | Last updated: 2026-05-18*