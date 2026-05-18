# How To: High Variance Confounds C F

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Check C and F order give same result.

They might take different paths in the function.

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

### Step 1: 'Check C and F order give same result.\n\n    They might take different paths in the function.\n    '

```python
'Check C and F order give same result.\n\n    They might take different paths in the function.\n    '
```

**Verification:**
```python
assert_almost_equal(seriesC, seriesF, decimal=13)
```

### Step 2: Assign n_features = 1001

```python
n_features = 1001
```

**Verification:**
```python
assert_almost_equal(outC, outF, decimal=13)
```

### Step 3: Assign length = 20

```python
length = 20
```

### Step 4: Assign n_confounds = 5

```python
n_confounds = 5
```

### Step 5: Assign unknown = generate_signals(...)

```python
seriesC, _, _ = generate_signals(n_features=n_features, length=length, order='C')
```

### Step 6: Assign unknown = generate_signals(...)

```python
seriesF, _, _ = generate_signals(n_features=n_features, length=length, order='F')
```

### Step 7: Call assert_almost_equal()

```python
assert_almost_equal(seriesC, seriesF, decimal=13)
```

### Step 8: Assign outC = high_variance_confounds(...)

```python
outC = high_variance_confounds(seriesC, n_confounds=n_confounds, detrend=False)
```

### Step 9: Assign outF = high_variance_confounds(...)

```python
outF = high_variance_confounds(seriesF, n_confounds=n_confounds, detrend=False)
```

### Step 10: Call assert_almost_equal()

```python
assert_almost_equal(outC, outF, decimal=13)
```


## Complete Example

```python
# Workflow
'Check C and F order give same result.\n\n    They might take different paths in the function.\n    '
n_features = 1001
length = 20
n_confounds = 5
seriesC, _, _ = generate_signals(n_features=n_features, length=length, order='C')
seriesF, _, _ = generate_signals(n_features=n_features, length=length, order='F')
assert_almost_equal(seriesC, seriesF, decimal=13)
outC = high_variance_confounds(seriesC, n_confounds=n_confounds, detrend=False)
outF = high_variance_confounds(seriesF, n_confounds=n_confounds, detrend=False)
assert_almost_equal(outC, outF, decimal=13)
```

## Next Steps


---

*Source: test_signal.py:1130 | Complexity: Advanced | Last updated: 2026-05-18*