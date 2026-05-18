# How To: Detrend

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test custom detrend implementation.

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

### Step 1: 'Test custom detrend implementation.'

```python
'Test custom detrend implementation.'
```

**Verification:**
```python
assert abs(detrended.mean(axis=0)).max() < 15.0 * EPS
```

### Step 2: Assign point_number = 703

```python
point_number = 703
```

**Verification:**
```python
assert_almost_equal(original, x, decimal=14)
```

### Step 3: Assign features = 17

```python
features = 17
```

**Verification:**
```python
assert abs(detrended.mean(axis=0)).max() < 15.0 * EPS
```

### Step 4: Assign unknown = generate_signals(...)

```python
signals, _, _ = generate_signals(n_features=features, length=point_number, same_variance=True)
```

**Verification:**
```python
assert_almost_equal(detrended_scipy, detrended, decimal=14)
```

### Step 5: Assign trends = generate_trends(...)

```python
trends = generate_trends(n_features=features, length=point_number)
```

**Verification:**
```python
assert_almost_equal(detrended, signals, decimal=14)
```

### Step 6: Assign x = value

```python
x = signals + trends + 1
```

**Verification:**
```python
assert abs(x.mean(axis=0)).max() < 15.0 * EPS
```

### Step 7: Assign original = x.copy(...)

```python
original = x.copy()
```

**Verification:**
```python
assert_almost_equal(detrended_scipy, detrended, decimal=14)
```

### Step 8: Assign detrended = _detrend(...)

```python
detrended = _detrend(x, inplace=False, type='constant')
```

**Verification:**
```python
assert_almost_equal(x, signals, decimal=14)
```

### Step 9: Assign detrended = _detrend(...)

```python
detrended = _detrend(x, inplace=False)
```

**Verification:**
```python
assert_array_equal(length_1_signal, _detrend(length_1_signal))
```

### Step 10: Assign detrended_scipy = scipy.signal.detrend(...)

```python
detrended_scipy = scipy.signal.detrend(x, axis=0)
```

**Verification:**
```python
assert abs(detrended.mean(axis=0)).max() < 20.0 * EPS
```

### Step 11: Call assert_almost_equal()

```python
assert_almost_equal(original, x, decimal=14)
```

**Verification:**
```python
assert abs(detrended.mean(axis=0)).max() < 15.0 * EPS
```

### Step 12: Call assert_almost_equal()

```python
assert_almost_equal(detrended_scipy, detrended, decimal=14)
```

### Step 13: Call assert_almost_equal()

```python
assert_almost_equal(detrended, signals, decimal=14)
```

### Step 14: Call _detrend()

```python
_detrend(x, inplace=True)
```

**Verification:**
```python
assert abs(x.mean(axis=0)).max() < 15.0 * EPS
```

### Step 15: Call assert_almost_equal()

```python
assert_almost_equal(detrended_scipy, detrended, decimal=14)
```

### Step 16: Call assert_almost_equal()

```python
assert_almost_equal(x, signals, decimal=14)
```

### Step 17: Assign length_1_signal = value

```python
length_1_signal = x[0]
```

### Step 18: Assign length_1_signal = value

```python
length_1_signal = length_1_signal[np.newaxis, :]
```

### Step 19: Call assert_array_equal()

```python
assert_array_equal(length_1_signal, _detrend(length_1_signal))
```

### Step 20: Assign detrended = _detrend(...)

```python
detrended = _detrend(x.astype(np.int64), inplace=True, type='constant')
```

**Verification:**
```python
assert abs(detrended.mean(axis=0)).max() < 20.0 * EPS
```


## Complete Example

```python
# Workflow
'Test custom detrend implementation.'
point_number = 703
features = 17
signals, _, _ = generate_signals(n_features=features, length=point_number, same_variance=True)
trends = generate_trends(n_features=features, length=point_number)
x = signals + trends + 1
original = x.copy()
detrended = _detrend(x, inplace=False, type='constant')
assert abs(detrended.mean(axis=0)).max() < 15.0 * EPS
detrended = _detrend(x, inplace=False)
detrended_scipy = scipy.signal.detrend(x, axis=0)
assert_almost_equal(original, x, decimal=14)
assert abs(detrended.mean(axis=0)).max() < 15.0 * EPS
assert_almost_equal(detrended_scipy, detrended, decimal=14)
assert_almost_equal(detrended, signals, decimal=14)
_detrend(x, inplace=True)
assert abs(x.mean(axis=0)).max() < 15.0 * EPS
assert_almost_equal(detrended_scipy, detrended, decimal=14)
assert_almost_equal(x, signals, decimal=14)
length_1_signal = x[0]
length_1_signal = length_1_signal[np.newaxis, :]
assert_array_equal(length_1_signal, _detrend(length_1_signal))
detrended = _detrend(x.astype(np.int64), inplace=True, type='constant')
assert abs(detrended.mean(axis=0)).max() < 20.0 * EPS
```

## Next Steps


---

*Source: test_signal.py:412 | Complexity: Advanced | Last updated: 2026-05-18*