# How To: Standardize

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test standardize_signal with several options.

## Prerequisites

- [ ] Setup code must be executed first

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

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: 'Test standardize_signal with several options.'

```python
'Test standardize_signal with several options.'
```

**Verification:**
```python
assert corr_coef_feature.mean() == 1
```

### Step 2: Assign n_features = 10

```python
n_features = 10
```

**Verification:**
```python
assert_almost_equal(stds, np.ones(n_features), decimal=1)
```

### Step 3: Assign n_samples = 17

```python
n_samples = 17
```

**Verification:**
```python
assert_almost_equal(b.sum(axis=0), np.zeros(n_features))
```

### Step 4: Assign a = rng.random(...)

```python
a = rng.random((n_samples, n_features))
```

**Verification:**
```python
assert_almost_equal(b, np.zeros(b.shape))
```

### Step 5: Assign z = standardize_signal(...)

```python
z = standardize_signal(a)
```

**Verification:**
```python
assert_almost_equal(b, np.zeros(b.shape))
```

### Step 6: Assign psc = standardize_signal(...)

```python
psc = standardize_signal(a, standardize='psc')
```

**Verification:**
```python
assert_array_equal(length_1_signal, standardize_signal(length_1_signal))
```

### Step 7: Assign corr_coef_feature = value

```python
corr_coef_feature = np.corrcoef(z[:, 0], psc[:, 0])[0, 1]
```

**Verification:**
```python
assert corr_coef_feature.mean() == 1
```

### Step 8: Assign b = standardize_signal(...)

```python
b = standardize_signal(a)
```

### Step 9: Assign stds = np.std(...)

```python
stds = np.std(b)
```

### Step 10: Call assert_almost_equal()

```python
assert_almost_equal(stds, np.ones(n_features), decimal=1)
```

### Step 11: Call assert_almost_equal()

```python
assert_almost_equal(b.sum(axis=0), np.zeros(n_features))
```

### Step 12: Assign a = value

```python
a = np.atleast_2d(np.linspace(0, 2.0, n_features)).T
```

### Step 13: Assign b = standardize_signal(...)

```python
b = standardize_signal(a, detrend=True, standardize=None)
```

### Step 14: Call assert_almost_equal()

```python
assert_almost_equal(b, np.zeros(b.shape))
```

### Step 15: Assign b = standardize_signal(...)

```python
b = standardize_signal(a, detrend=True)
```

### Step 16: Call assert_almost_equal()

```python
assert_almost_equal(b, np.zeros(b.shape))
```

### Step 17: Assign length_1_signal = np.atleast_2d(...)

```python
length_1_signal = np.atleast_2d(np.linspace(0, 2.0, n_features))
```

### Step 18: Call assert_array_equal()

```python
assert_array_equal(length_1_signal, standardize_signal(length_1_signal))
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
'Test standardize_signal with several options.'
n_features = 10
n_samples = 17
a = rng.random((n_samples, n_features))
a += np.linspace(0, 2.0, n_features)
z = standardize_signal(a)
psc = standardize_signal(a, standardize='psc')
corr_coef_feature = np.corrcoef(z[:, 0], psc[:, 0])[0, 1]
assert corr_coef_feature.mean() == 1
b = standardize_signal(a)
stds = np.std(b)
assert_almost_equal(stds, np.ones(n_features), decimal=1)
assert_almost_equal(b.sum(axis=0), np.zeros(n_features))
a = np.atleast_2d(np.linspace(0, 2.0, n_features)).T
b = standardize_signal(a, detrend=True, standardize=None)
assert_almost_equal(b, np.zeros(b.shape))
b = standardize_signal(a, detrend=True)
assert_almost_equal(b, np.zeros(b.shape))
length_1_signal = np.atleast_2d(np.linspace(0, 2.0, n_features))
assert_array_equal(length_1_signal, standardize_signal(length_1_signal))
```

## Next Steps


---

*Source: test_signal.py:344 | Complexity: Advanced | Last updated: 2026-05-18*