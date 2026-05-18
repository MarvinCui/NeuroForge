# How To: Clean Confounds Detrending

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test detrending.

No trend should exist in the output.

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

### Step 1: 'Test detrending.\n\n    No trend should exist in the output.\n    '

```python
'Test detrending.\n\n    No trend should exist in the output.\n    '
```

**Verification:**
```python
assert (abs(coeffs) > 0.001).any()
```

### Step 2: Assign unknown = generate_signals(...)

```python
signals, noises, confounds = generate_signals(n_features=41, n_confounds=5, length=45)
```

**Verification:**
```python
assert (abs(coeffs) < 1000.0 * EPS).all()
```

### Step 3: Assign temp = value

```python
temp = confounds.T
```

### Step 4: Assign cleaned_signals = clean(...)

```python
cleaned_signals = clean(signals + noises, confounds=confounds, detrend=False, standardize=None)
```

### Step 5: Assign coeffs = np.polyfit(...)

```python
coeffs = np.polyfit(np.arange(cleaned_signals.shape[0]), cleaned_signals, 1)
```

**Verification:**
```python
assert (abs(coeffs) > 0.001).any()
```

### Step 6: Assign cleaned_signals = clean(...)

```python
cleaned_signals = clean(signals + noises, confounds=confounds, detrend=True, standardize=None)
```

### Step 7: Assign coeffs = np.polyfit(...)

```python
coeffs = np.polyfit(np.arange(cleaned_signals.shape[0]), cleaned_signals, 1)
```

**Verification:**
```python
assert (abs(coeffs) < 1000.0 * EPS).all()
```


## Complete Example

```python
# Workflow
'Test detrending.\n\n    No trend should exist in the output.\n    '
signals, noises, confounds = generate_signals(n_features=41, n_confounds=5, length=45)
temp = confounds.T
temp += np.arange(confounds.shape[0])
cleaned_signals = clean(signals + noises, confounds=confounds, detrend=False, standardize=None)
coeffs = np.polyfit(np.arange(cleaned_signals.shape[0]), cleaned_signals, 1)
assert (abs(coeffs) > 0.001).any()
cleaned_signals = clean(signals + noises, confounds=confounds, detrend=True, standardize=None)
coeffs = np.polyfit(np.arange(cleaned_signals.shape[0]), cleaned_signals, 1)
assert (abs(coeffs) < 1000.0 * EPS).all()
```

## Next Steps


---

*Source: test_signal.py:838 | Complexity: Intermediate | Last updated: 2026-05-18*