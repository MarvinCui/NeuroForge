# How To: Inverse Coef

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test inverse coefficients computation.

## Prerequisites

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `numpy`
- `numpy.fft`
- `numpy.testing`
- `sklearn.linear_model`
- `sklearn.utils.estimator_checks`
- `mne.decoding`
- `mne.decoding.receptive_field`
- `mne.decoding.time_delaying_ridge`
- `mne.fixes`


## Step-by-Step Guide

### Step 1: 'Test inverse coefficients computation.'

```python
'Test inverse coefficients computation.'
```

**Verification:**
```python
assert_array_equal(rf.coef_.shape, rf.patterns_.shape, (n_targets, n_feats, n_delays))
```

### Step 2: Assign unknown = value

```python
tmin, tmax = (0.0, 10.0)
```

**Verification:**
```python
assert_array_equal(inv_rf.coef_.shape, inv_rf.patterns_.shape, (n_feats, n_targets, n_delays))
```

### Step 3: Assign unknown = value

```python
n_feats, n_targets, n_samples = (3, 2, 1000)
```

**Verification:**
```python
assert_allclose(np.dot(c0, c1.T), np.eye(c0.shape[0]), atol=0.2)
```

### Step 4: Assign n_delays = int(...)

```python
n_delays = int(tmax - tmin + 1)
```

### Step 5: Assign unknown = _make_data(...)

```python
X, y = _make_data(n_feats, n_targets, n_samples, tmin, tmax)
```

### Step 6: Assign tdr = TimeDelayingRidge(...)

```python
tdr = TimeDelayingRidge(tmin, tmax, 1.0, 0.1, 'laplacian')
```

### Step 7: Assign rf = ReceptiveField(...)

```python
rf = ReceptiveField(tmin, tmax, 1.0, estimator=estimator, patterns=True)
```

### Step 8: Call rf.fit()

```python
rf.fit(X, y)
```

### Step 9: Assign inv_rf = ReceptiveField(...)

```python
inv_rf = ReceptiveField(tmin, tmax, 1.0, estimator=estimator, patterns=True)
```

### Step 10: Call inv_rf.fit()

```python
inv_rf.fit(y, X)
```

### Step 11: Call assert_array_equal()

```python
assert_array_equal(rf.coef_.shape, rf.patterns_.shape, (n_targets, n_feats, n_delays))
```

### Step 12: Call assert_array_equal()

```python
assert_array_equal(inv_rf.coef_.shape, inv_rf.patterns_.shape, (n_feats, n_targets, n_delays))
```

### Step 13: Assign c0 = rf.coef_.reshape(...)

```python
c0 = rf.coef_.reshape(n_targets, n_feats * n_delays)
```

### Step 14: Assign c1 = rf.patterns_.reshape(...)

```python
c1 = rf.patterns_.reshape(n_targets, n_feats * n_delays)
```

### Step 15: Call assert_allclose()

```python
assert_allclose(np.dot(c0, c1.T), np.eye(c0.shape[0]), atol=0.2)
```


## Complete Example

```python
# Workflow
'Test inverse coefficients computation.'
tmin, tmax = (0.0, 10.0)
n_feats, n_targets, n_samples = (3, 2, 1000)
n_delays = int(tmax - tmin + 1)
X, y = _make_data(n_feats, n_targets, n_samples, tmin, tmax)
tdr = TimeDelayingRidge(tmin, tmax, 1.0, 0.1, 'laplacian')
for estimator in (0.0, 0.01, Ridge(alpha=0.0), tdr):
    rf = ReceptiveField(tmin, tmax, 1.0, estimator=estimator, patterns=True)
    rf.fit(X, y)
    inv_rf = ReceptiveField(tmin, tmax, 1.0, estimator=estimator, patterns=True)
    inv_rf.fit(y, X)
    assert_array_equal(rf.coef_.shape, rf.patterns_.shape, (n_targets, n_feats, n_delays))
    assert_array_equal(inv_rf.coef_.shape, inv_rf.patterns_.shape, (n_feats, n_targets, n_delays))
    c0 = rf.coef_.reshape(n_targets, n_feats * n_delays)
    c1 = rf.patterns_.reshape(n_targets, n_feats * n_delays)
    assert_allclose(np.dot(c0, c1.T), np.eye(c0.shape[0]), atol=0.2)
```

## Next Steps


---

*Source: test_receptive_field.py:550 | Complexity: Advanced | Last updated: 2026-05-18*