# How To: Compute Nearest

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test nearest neighbor searches.

## Prerequisites

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne.channels`
- `mne.datasets`
- `mne.io`
- `mne.surface`
- `mne.transforms`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test nearest neighbor searches.'

```python
'Test nearest neighbor searches.'
```

**Verification:**
```python
assert_array_equal(nn_true, nn1)
```

### Step 2: Assign x = rng.randn(...)

```python
x = rng.randn(500, 3)
```

**Verification:**
```python
assert_array_equal(nn_true, nn2)
```

### Step 3: Assign nn_true = value

```python
nn_true = rng.permutation(np.arange(500, dtype=np.int64))[:20]
```

**Verification:**
```python
assert_array_equal(nn_true, nn3)
```

### Step 4: Assign y = value

```python
y = x[nn_true]
```

**Verification:**
```python
assert_array_equal(nnn1[0], nn_true)
```

### Step 5: Assign nn1 = _compute_nearest(...)

```python
nn1 = _compute_nearest(x, y, method='BallTree')
```

**Verification:**
```python
assert_array_equal(nnn1[1], np.zeros_like(nn1))
```

### Step 6: Assign nn2 = _compute_nearest(...)

```python
nn2 = _compute_nearest(x, y, method='KDTree')
```

**Verification:**
```python
assert_equal(len(nnn1), len(nnn2))
```

### Step 7: Assign nn3 = _compute_nearest(...)

```python
nn3 = _compute_nearest(x, y, method='cdist')
```

**Verification:**
```python
assert_array_equal(nn1, nn2)
```

### Step 8: Call assert_array_equal()

```python
assert_array_equal(nn_true, nn1)
```

**Verification:**
```python
assert_array_equal(nn1, nn3)
```

### Step 9: Call assert_array_equal()

```python
assert_array_equal(nn_true, nn2)
```

### Step 10: Call assert_array_equal()

```python
assert_array_equal(nn_true, nn3)
```

### Step 11: Assign nnn1 = _compute_nearest(...)

```python
nnn1 = _compute_nearest(x, y, method='BallTree', return_dists=True)
```

### Step 12: Assign nnn2 = _compute_nearest(...)

```python
nnn2 = _compute_nearest(x, y, method='KDTree', return_dists=True)
```

### Step 13: Assign nnn3 = _compute_nearest(...)

```python
nnn3 = _compute_nearest(x, y, method='cdist', return_dists=True)
```

### Step 14: Call assert_array_equal()

```python
assert_array_equal(nnn1[0], nn_true)
```

### Step 15: Call assert_array_equal()

```python
assert_array_equal(nnn1[1], np.zeros_like(nn1))
```

### Step 16: Call assert_equal()

```python
assert_equal(len(nnn1), len(nnn2))
```

### Step 17: Call assert_array_equal()

```python
assert_array_equal(nn1, nn2)
```

### Step 18: Call assert_array_equal()

```python
assert_array_equal(nn1, nn3)
```


## Complete Example

```python
# Workflow
'Test nearest neighbor searches.'
x = rng.randn(500, 3)
x /= np.sqrt(np.sum(x ** 2, axis=1))[:, None]
nn_true = rng.permutation(np.arange(500, dtype=np.int64))[:20]
y = x[nn_true]
nn1 = _compute_nearest(x, y, method='BallTree')
nn2 = _compute_nearest(x, y, method='KDTree')
nn3 = _compute_nearest(x, y, method='cdist')
assert_array_equal(nn_true, nn1)
assert_array_equal(nn_true, nn2)
assert_array_equal(nn_true, nn3)
nnn1 = _compute_nearest(x, y, method='BallTree', return_dists=True)
nnn2 = _compute_nearest(x, y, method='KDTree', return_dists=True)
nnn3 = _compute_nearest(x, y, method='cdist', return_dists=True)
assert_array_equal(nnn1[0], nn_true)
assert_array_equal(nnn1[1], np.zeros_like(nn1))
assert_equal(len(nnn1), len(nnn2))
for nn1, nn2, nn3 in zip(nnn1, nnn2, nnn3):
    assert_array_equal(nn1, nn2)
    assert_array_equal(nn1, nn3)
```

## Next Steps


---

*Source: test_surface.py:100 | Complexity: Advanced | Last updated: 2026-05-18*