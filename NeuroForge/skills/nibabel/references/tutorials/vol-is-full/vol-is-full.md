# How To: Vol Is Full

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test vol is full

## Prerequisites

**Required Modules:**
- `glob`
- `os.path`
- `os.path`
- `warnings`
- `numpy`
- `pytest`
- `numpy`
- `numpy.testing`
- `fileholders`
- `nifti1`
- `openers`
- `parrec`
- `testing`
- `volumeutils`
- `test_arrayproxy`


## Step-by-Step Guide

### Step 1: Call assert_array_equal()

```python
assert_array_equal(vol_is_full([3, 2, 1], 3), True)
```

**Verification:**
```python
assert_array_equal(vol_is_full([3, 2, 1], 3), True)
```

### Step 2: Call assert_array_equal()

```python
assert_array_equal(vol_is_full([3, 2, 1], 4), False)
```

**Verification:**
```python
assert_array_equal(vol_is_full([3, 2, 1], 4), False)
```

### Step 3: Call assert_array_equal()

```python
assert_array_equal(vol_is_full([4, 2, 1], 4), False)
```

**Verification:**
```python
assert_array_equal(vol_is_full([4, 2, 1], 4), False)
```

### Step 4: Call assert_array_equal()

```python
assert_array_equal(vol_is_full([3, 2, 4, 1], 4), True)
```

**Verification:**
```python
assert_array_equal(vol_is_full([3, 2, 4, 1], 4), True)
```

### Step 5: Call assert_array_equal()

```python
assert_array_equal(vol_is_full([3, 2, 1], 3, 0), False)
```

**Verification:**
```python
assert_array_equal(vol_is_full([3, 2, 1], 3, 0), False)
```

### Step 6: Call assert_array_equal()

```python
assert_array_equal(vol_is_full([3, 2, 0, 1], 3, 0), True)
```

**Verification:**
```python
assert_array_equal(vol_is_full([3, 2, 0, 1], 3, 0), True)
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(vol_is_full([3, 2, 1, 2, 3, 1], 3), [True] * 6)
```

**Verification:**
```python
assert_array_equal(vol_is_full([3, 2, 1, 2, 3, 1], 3), [True] * 6)
```

### Step 8: Call assert_array_equal()

```python
assert_array_equal(vol_is_full([3, 2, 1, 2, 3], 3), [True, True, True, False, False])
```

**Verification:**
```python
assert_array_equal(vol_is_full([3, 2, 1, 2, 3], 3), [True, True, True, False, False])
```

### Step 9: Call vol_is_full()

```python
vol_is_full([2, 1, 0], 2)
```

### Step 10: Call vol_is_full()

```python
vol_is_full([3, 2, 1], 3, 2)
```


## Complete Example

```python
# Workflow
assert_array_equal(vol_is_full([3, 2, 1], 3), True)
assert_array_equal(vol_is_full([3, 2, 1], 4), False)
assert_array_equal(vol_is_full([4, 2, 1], 4), False)
assert_array_equal(vol_is_full([3, 2, 4, 1], 4), True)
assert_array_equal(vol_is_full([3, 2, 1], 3, 0), False)
assert_array_equal(vol_is_full([3, 2, 0, 1], 3, 0), True)
with pytest.raises(ValueError):
    vol_is_full([2, 1, 0], 2)
with pytest.raises(ValueError):
    vol_is_full([3, 2, 1], 3, 2)
assert_array_equal(vol_is_full([3, 2, 1, 2, 3, 1], 3), [True] * 6)
assert_array_equal(vol_is_full([3, 2, 1, 2, 3], 3), [True, True, True, False, False])
```

## Next Steps


---

*Source: test_parrec.py:445 | Complexity: Advanced | Last updated: 2026-05-18*