# How To: Infomax Weights Ini

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test the infomax algorithm w/initial weights matrix.

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `mne.preprocessing.infomax_`
- `mne.utils`
- `sklearn.decomposition`


## Step-by-Step Guide

### Step 1: 'Test the infomax algorithm w/initial weights matrix.'

```python
'Test the infomax algorithm w/initial weights matrix.'
```

**Verification:**
```python
assert_almost_equal(w1, weights)
```

### Step 2: Assign X = np.random.random(...)

```python
X = np.random.random((3, 100))
```

**Verification:**
```python
assert_almost_equal(w2, weights)
```

### Step 3: Assign weights = np.array(...)

```python
weights = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]], dtype=np.float64)
```

### Step 4: Assign w1 = infomax(...)

```python
w1 = infomax(X, max_iter=0, weights=weights, extended=True)
```

### Step 5: Assign w2 = infomax(...)

```python
w2 = infomax(X, max_iter=0, weights=weights, extended=False)
```

### Step 6: Call assert_almost_equal()

```python
assert_almost_equal(w1, weights)
```

### Step 7: Call assert_almost_equal()

```python
assert_almost_equal(w2, weights)
```


## Complete Example

```python
# Workflow
'Test the infomax algorithm w/initial weights matrix.'
X = np.random.random((3, 100))
weights = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]], dtype=np.float64)
w1 = infomax(X, max_iter=0, weights=weights, extended=True)
w2 = infomax(X, max_iter=0, weights=weights, extended=False)
assert_almost_equal(w1, weights)
assert_almost_equal(w2, weights)
```

## Next Steps


---

*Source: test_infomax.py:121 | Complexity: Intermediate | Last updated: 2026-05-18*