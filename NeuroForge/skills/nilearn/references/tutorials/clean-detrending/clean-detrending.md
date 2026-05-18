# How To: Clean Detrending

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Check effect of clean with detrending.

This test is inspired from Scipy docstring of detrend function.

- clean should not modify inputs
- check effect when fintie results requested

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

### Step 1: 'Check effect of clean with detrending.\n\n    This test is inspired from Scipy docstring of detrend function.\n\n    - clean should not modify inputs\n    - check effect when fintie results requested\n    '

```python
'Check effect of clean with detrending.\n\n    This test is inspired from Scipy docstring of detrend function.\n\n    - clean should not modify inputs\n    - check effect when fintie results requested\n    '
```

**Verification:**
```python
assert np.any(np.isfinite(y_clean))
```

### Step 2: Assign n_samples = 21

```python
n_samples = 21
```

**Verification:**
```python
assert_almost_equal(y_orig, y, decimal=13)
```

### Step 3: Assign n_features = 501

```python
n_features = 501
```

**Verification:**
```python
assert_almost_equal(x_detrended, signals, decimal=13)
```

### Step 4: Assign unknown = generate_signals(...)

```python
signals, _, _ = generate_signals(n_features=n_features, length=n_samples)
```

**Verification:**
```python
assert array_equal(x_orig, x)
```

### Step 5: Assign trends = generate_trends(...)

```python
trends = generate_trends(n_features=n_features, length=n_samples)
```

**Verification:**
```python
assert abs(x_undetrended - signals).max() >= 0.06
```

### Step 6: Assign x = value

```python
x = signals + trends
```

**Verification:**
```python
assert array_equal(x_orig, x)
```

### Step 7: Assign x_orig = x.copy(...)

```python
x_orig = x.copy()
```

### Step 8: Assign y = value

```python
y = signals + trends
```

### Step 9: Assign unknown = value

```python
y[20, 150] = np.nan
```

### Step 10: Assign unknown = value

```python
y[5, 500] = np.nan
```

### Step 11: Assign unknown = value

```python
y[15, 14] = np.inf
```

### Step 12: Assign y_orig = y.copy(...)

```python
y_orig = y.copy()
```

### Step 13: Assign y_clean = clean(...)

```python
y_clean = clean(y, ensure_finite=True)
```

**Verification:**
```python
assert np.any(np.isfinite(y_clean))
```

### Step 14: Call assert_almost_equal()

```python
assert_almost_equal(y_orig, y, decimal=13)
```

### Step 15: Assign match = "boolean values for 'standardize' will be deprecated"

```python
match = "boolean values for 'standardize' will be deprecated"
```

### Step 16: Call assert_almost_equal()

```python
assert_almost_equal(x_detrended, signals, decimal=13)
```

**Verification:**
```python
assert array_equal(x_orig, x)
```

### Step 17: Assign x_undetrended = clean(...)

```python
x_undetrended = clean(x, standardize=None, detrend=False)
```

**Verification:**
```python
assert abs(x_undetrended - signals).max() >= 0.06
```

### Step 18: Assign x_detrended = clean(...)

```python
x_detrended = clean(x, standardize=False)
```


## Complete Example

```python
# Workflow
'Check effect of clean with detrending.\n\n    This test is inspired from Scipy docstring of detrend function.\n\n    - clean should not modify inputs\n    - check effect when fintie results requested\n    '
n_samples = 21
n_features = 501
signals, _, _ = generate_signals(n_features=n_features, length=n_samples)
trends = generate_trends(n_features=n_features, length=n_samples)
x = signals + trends
x_orig = x.copy()
y = signals + trends
y[20, 150] = np.nan
y[5, 500] = np.nan
y[15, 14] = np.inf
y_orig = y.copy()
y_clean = clean(y, ensure_finite=True)
assert np.any(np.isfinite(y_clean))
assert_almost_equal(y_orig, y, decimal=13)
match = "boolean values for 'standardize' will be deprecated"
with pytest.warns(FutureWarning, match=match):
    x_detrended = clean(x, standardize=False)
assert_almost_equal(x_detrended, signals, decimal=13)
assert array_equal(x_orig, x)
x_undetrended = clean(x, standardize=None, detrend=False)
assert abs(x_undetrended - signals).max() >= 0.06
assert array_equal(x_orig, x)
```

## Next Steps


---

*Source: test_signal.py:491 | Complexity: Advanced | Last updated: 2026-05-18*