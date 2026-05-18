# How To: Continuous Regression With Overlap

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test regression with overlap correction.

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy.signal.windows`
- `mne`
- `mne`
- `mne.datasets`
- `mne.io`
- `mne.stats.regression`
- `sklearn.linear_model`


## Step-by-Step Guide

### Step 1: 'Test regression with overlap correction.'

```python
'Test regression with overlap correction.'
```

**Verification:**
```python
assert_allclose(effect, linear_regression_raw(raw, events, {1: 1}, tmin=0)[1].data.flatten())
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('sklearn')
```

**Verification:**
```python
assert_allclose(effect, linear_regression_raw(raw, events, tmin=0, solver=solver)['1'].data.flatten())
```

### Step 3: Assign signal = np.zeros(...)

```python
signal = np.zeros(100000)
```

### Step 4: Assign times = value

```python
times = [1000, 2500, 3000, 5000, 5250, 7000, 7250, 8000]
```

### Step 5: Assign events = np.zeros(...)

```python
events = np.zeros((len(times), 3), int)
```

### Step 6: Assign unknown = 1

```python
events[:, 2] = 1
```

### Step 7: Assign unknown = times

```python
events[:, 0] = times
```

### Step 8: Assign unknown = 1.0

```python
signal[events[:, 0]] = 1.0
```

### Step 9: Assign effect = hann(...)

```python
effect = hann(101)
```

### Step 10: Assign signal = value

```python
signal = np.convolve(signal, effect)[:len(signal)]
```

### Step 11: Assign raw = RawArray(...)

```python
raw = RawArray(signal[np.newaxis, :], mne.create_info(1, 100, 'eeg'))
```

### Step 12: Call assert_allclose()

```python
assert_allclose(effect, linear_regression_raw(raw, events, {1: 1}, tmin=0)[1].data.flatten())
```

### Step 13: Call assert_allclose()

```python
assert_allclose(effect, linear_regression_raw(raw, events, tmin=0, solver=solver)['1'].data.flatten())
```

### Step 14: Call pytest.raises()

```python
pytest.raises(ValueError, linear_regression_raw, raw, events, solver=solT)
```

### Step 15: Call pytest.raises()

```python
pytest.raises(ValueError, linear_regression_raw, raw, events, solver='err')
```

### Step 16: Call pytest.raises()

```python
pytest.raises(TypeError, linear_regression_raw, raw, events, solver=0)
```


## Complete Example

```python
# Workflow
'Test regression with overlap correction.'
pytest.importorskip('sklearn')
signal = np.zeros(100000)
times = [1000, 2500, 3000, 5000, 5250, 7000, 7250, 8000]
events = np.zeros((len(times), 3), int)
events[:, 2] = 1
events[:, 0] = times
signal[events[:, 0]] = 1.0
effect = hann(101)
signal = np.convolve(signal, effect)[:len(signal)]
raw = RawArray(signal[np.newaxis, :], mne.create_info(1, 100, 'eeg'))
assert_allclose(effect, linear_regression_raw(raw, events, {1: 1}, tmin=0)[1].data.flatten())
from sklearn.linear_model import ridge_regression

def solver(X, y):
    return np.atleast_2d(ridge_regression(X, y, alpha=0.0, solver='cholesky'))
assert_allclose(effect, linear_regression_raw(raw, events, tmin=0, solver=solver)['1'].data.flatten())

def solT(X, y):
    return ridge_regression(X, y, alpha=0.0, solver='cholesky').T
pytest.raises(ValueError, linear_regression_raw, raw, events, solver=solT)
pytest.raises(ValueError, linear_regression_raw, raw, events, solver='err')
pytest.raises(TypeError, linear_regression_raw, raw, events, solver=0)
```

## Next Steps


---

*Source: test_regression.py:121 | Complexity: Advanced | Last updated: 2026-05-18*