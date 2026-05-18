# How To: Mean Of Squares

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test _mean_of_squares.

## Prerequisites

**Required Modules:**
- `pathlib`
- `typing`
- `numpy`
- `pytest`
- `scipy.signal`
- `numpy`
- `numpy.testing`
- `pandas`
- `nilearn.conftest`
- `nilearn.exceptions`
- `nilearn.signal`


## Step-by-Step Guide

### Step 1: 'Test _mean_of_squares.'

```python
'Test _mean_of_squares.'
```

**Verification:**
```python
assert_almost_equal(var1, var2)
```

### Step 2: Assign n_samples = 11

```python
n_samples = 11
```

### Step 3: Assign n_features = 501

```python
n_features = 501
```

### Step 4: Assign unknown = generate_signals(...)

```python
signals, _, _ = generate_signals(n_features=n_features, length=n_samples, same_variance=True)
```

### Step 5: Assign var1 = np.copy(...)

```python
var1 = np.copy(signals)
```

### Step 6: Assign var1 = var1.mean(...)

```python
var1 = var1.mean(axis=0)
```

### Step 7: Assign var2 = _mean_of_squares(...)

```python
var2 = _mean_of_squares(signals)
```

### Step 8: Call assert_almost_equal()

```python
assert_almost_equal(var1, var2)
```


## Complete Example

```python
# Workflow
'Test _mean_of_squares.'
n_samples = 11
n_features = 501
signals, _, _ = generate_signals(n_features=n_features, length=n_samples, same_variance=True)
var1 = np.copy(signals)
var1 **= 2
var1 = var1.mean(axis=0)
var2 = _mean_of_squares(signals)
assert_almost_equal(var1, var2)
```

## Next Steps


---

*Source: test_signal.py:458 | Complexity: Advanced | Last updated: 2026-05-18*