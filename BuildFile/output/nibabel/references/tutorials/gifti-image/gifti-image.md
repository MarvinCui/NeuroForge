# How To: Gifti Image

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test gifti image

## Prerequisites

**Required Modules:**
- `itertools`
- `sys`
- `io`
- `numpy`
- `pytest`
- `numpy.testing`
- `nibabel.tmpdirs`
- `fileholders`
- `nifti1`
- `testing`
- `test_parse_gifti_fast`
- `gifti`


## Step-by-Step Guide

### Step 1: Assign gi = GiftiImage(...)

```python
gi = GiftiImage()
```

**Verification:**
```python
assert gi.darrays == []
```

### Step 2: Assign arr = np.zeros(...)

```python
arr = np.zeros((2, 3))
```

**Verification:**
```python
assert gi.meta == {}
```

### Step 3: Call gi.darrays.append()

```python
gi.darrays.append(arr)
```

**Verification:**
```python
assert gi.labeltable.labels == []
```

### Step 4: Assign gi = GiftiImage(...)

```python
gi = GiftiImage()
```

**Verification:**
```python
assert gi.darrays == []
```

### Step 5: Assign gi = GiftiImage(...)

```python
gi = GiftiImage()
```

**Verification:**
```python
assert gi.numDA == 0
```

### Step 6: Assign data = rng.random(...)

```python
data = rng.random(5, dtype=np.float32)
```

**Verification:**
```python
assert gi.numDA == 1
```

### Step 7: Assign da = GiftiDataArray(...)

```python
da = GiftiDataArray(data)
```

**Verification:**
```python
assert_array_equal(gi.darrays[0].data, data)
```

### Step 8: Call gi.add_gifti_data_array()

```python
gi.add_gifti_data_array(da)
```

**Verification:**
```python
assert gi.numDA == 0
```

### Step 9: Call assert_array_equal()

```python
assert_array_equal(gi.darrays[0].data, data)
```

**Verification:**
```python
assert gi.numDA == 0
```

### Step 10: Call gi.remove_gifti_data_array()

```python
gi.remove_gifti_data_array(0)
```

**Verification:**
```python
assert gi.numDA == 1, "data array should exist on 'missed' remove"
```

### Step 11: Assign gi = GiftiImage(...)

```python
gi = GiftiImage()
```

**Verification:**
```python
assert gi.numDA == 0
```

### Step 12: Call gi.remove_gifti_data_array_by_intent()

```python
gi.remove_gifti_data_array_by_intent(0)
```

**Verification:**
```python
assert gi.numDA == 0
```

### Step 13: Assign gi = GiftiImage(...)

```python
gi = GiftiImage()
```

### Step 14: Assign da = GiftiDataArray(...)

```python
da = GiftiDataArray(np.zeros((5,), np.float32), intent=0)
```

### Step 15: Call gi.add_gifti_data_array()

```python
gi.add_gifti_data_array(da)
```

### Step 16: Call gi.remove_gifti_data_array_by_intent()

```python
gi.remove_gifti_data_array_by_intent(3)
```

**Verification:**
```python
assert gi.numDA == 1, "data array should exist on 'missed' remove"
```

### Step 17: Call gi.remove_gifti_data_array_by_intent()

```python
gi.remove_gifti_data_array_by_intent(da.intent)
```

**Verification:**
```python
assert gi.numDA == 0
```


## Complete Example

```python
# Workflow
gi = GiftiImage()
assert gi.darrays == []
assert gi.meta == {}
assert gi.labeltable.labels == []
arr = np.zeros((2, 3))
gi.darrays.append(arr)
gi = GiftiImage()
assert gi.darrays == []
gi = GiftiImage()
assert gi.numDA == 0
data = rng.random(5, dtype=np.float32)
da = GiftiDataArray(data)
gi.add_gifti_data_array(da)
assert gi.numDA == 1
assert_array_equal(gi.darrays[0].data, data)
gi.remove_gifti_data_array(0)
assert gi.numDA == 0
gi = GiftiImage()
gi.remove_gifti_data_array_by_intent(0)
assert gi.numDA == 0
gi = GiftiImage()
da = GiftiDataArray(np.zeros((5,), np.float32), intent=0)
gi.add_gifti_data_array(da)
gi.remove_gifti_data_array_by_intent(3)
assert gi.numDA == 1, "data array should exist on 'missed' remove"
gi.remove_gifti_data_array_by_intent(da.intent)
assert gi.numDA == 0
```

## Next Steps


---

*Source: test_gifti.py:67 | Complexity: Advanced | Last updated: 2026-05-18*