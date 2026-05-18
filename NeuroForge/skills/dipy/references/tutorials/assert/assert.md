# How To: Assert

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test assert

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `sys`
- `warnings`
- `numpy`
- `numpy.testing`
- `dipy.testing`
- `dipy.testing.decorators`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Call npt.assert_raises()

```python
npt.assert_raises(AssertionError, dt.assert_false, True)
```

### Step 2: Call npt.assert_raises()

```python
npt.assert_raises(AssertionError, dt.assert_true, False)
```

### Step 3: Call npt.assert_raises()

```python
npt.assert_raises(AssertionError, dt.assert_less, 2, 1)
```

### Step 4: Call npt.assert_raises()

```python
npt.assert_raises(AssertionError, dt.assert_less_equal, 2, 1)
```

### Step 5: Call npt.assert_raises()

```python
npt.assert_raises(AssertionError, dt.assert_greater, 1, 2)
```

### Step 6: Call npt.assert_raises()

```python
npt.assert_raises(AssertionError, dt.assert_greater_equal, 1, 2)
```

### Step 7: Call npt.assert_raises()

```python
npt.assert_raises(AssertionError, dt.assert_not_equal, 5, 5)
```

### Step 8: Call npt.assert_raises()

```python
npt.assert_raises(AssertionError, dt.assert_operator, 2, 1)
```

### Step 9: Assign arr = value

```python
arr = [np.arange(k) for k in range(2, 12, 3)]
```

### Step 10: Assign arr2 = value

```python
arr2 = [np.arange(k) for k in range(2, 12, 4)]
```

### Step 11: Call npt.assert_raises()

```python
npt.assert_raises(AssertionError, dt.assert_arrays_equal, arr, arr2)
```

### Step 12: Assign arr = rng.random(...)

```python
arr = rng.random((100,))
```

### Step 13: Assign arr2 = arr.copy(...)

```python
arr2 = arr.copy()
```

### Step 14: Call npt.assert_raises()

```python
npt.assert_raises(AssertionError, dt.assert_percent_almost_equal, arr, arr2, decimal=5, percent=1.0)
```

### Step 15: Call dt.assert_percent_almost_equal()

```python
dt.assert_percent_almost_equal(arr, arr2, decimal=5, percent=0.99)
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
npt.assert_raises(AssertionError, dt.assert_false, True)
npt.assert_raises(AssertionError, dt.assert_true, False)
npt.assert_raises(AssertionError, dt.assert_less, 2, 1)
npt.assert_raises(AssertionError, dt.assert_less_equal, 2, 1)
npt.assert_raises(AssertionError, dt.assert_greater, 1, 2)
npt.assert_raises(AssertionError, dt.assert_greater_equal, 1, 2)
npt.assert_raises(AssertionError, dt.assert_not_equal, 5, 5)
npt.assert_raises(AssertionError, dt.assert_operator, 2, 1)
arr = [np.arange(k) for k in range(2, 12, 3)]
arr2 = [np.arange(k) for k in range(2, 12, 4)]
npt.assert_raises(AssertionError, dt.assert_arrays_equal, arr, arr2)
arr = rng.random((100,))
arr2 = arr.copy()
arr2[0] += 0.0001
npt.assert_raises(AssertionError, dt.assert_percent_almost_equal, arr, arr2, decimal=5, percent=1.0)
dt.assert_percent_almost_equal(arr, arr2, decimal=5, percent=0.99)
```

## Next Steps


---

*Source: test_testing.py:14 | Complexity: Advanced | Last updated: 2026-05-18*