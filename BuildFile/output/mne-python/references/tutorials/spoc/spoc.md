# How To: Spoc

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test SPoC.

## Prerequisites

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `sklearn.linear_model`
- `sklearn.model_selection`
- `sklearn.pipeline`
- `sklearn.svm`
- `sklearn.utils.estimator_checks`
- `mne`
- `mne.decoding`
- `mne.decoding.csp`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test SPoC.'

```python
'Test SPoC.'
```

**Verification:**
```python
assert_array_equal(Xt.shape, [10, 4])
```

### Step 2: Assign X = np.random.randn(...)

```python
X = np.random.randn(10, 10, 20)
```

**Verification:**
```python
assert_array_equal(Xt.shape, [10, 4, 20])
```

### Step 3: Assign y = np.random.randn(...)

```python
y = np.random.randn(10)
```

**Verification:**
```python
assert_array_equal(spoc.filters_.shape, [10, 10])
```

### Step 4: Assign spoc = SPoC(...)

```python
spoc = SPoC(n_components=4)
```

**Verification:**
```python
assert_array_equal(spoc.patterns_.shape, [10, 10])
```

### Step 5: Call spoc.fit()

```python
spoc.fit(X, y)
```

**Verification:**
```python
assert np.abs(corr) > 0.99
```

### Step 6: Assign Xt = spoc.transform(...)

```python
Xt = spoc.transform(X)
```

**Verification:**
```python
assert np.abs(corr) > 0.85
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(Xt.shape, [10, 4])
```

### Step 8: Assign spoc = SPoC(...)

```python
spoc = SPoC(n_components=4, transform_into='csp_space')
```

### Step 9: Call spoc.fit()

```python
spoc.fit(X, y)
```

### Step 10: Assign Xt = spoc.transform(...)

```python
Xt = spoc.transform(X)
```

### Step 11: Call assert_array_equal()

```python
assert_array_equal(Xt.shape, [10, 4, 20])
```

### Step 12: Call assert_array_equal()

```python
assert_array_equal(spoc.filters_.shape, [10, 10])
```

### Step 13: Call assert_array_equal()

```python
assert_array_equal(spoc.patterns_.shape, [10, 10])
```

### Step 14: Call pytest.raises()

```python
pytest.raises(ValueError, spoc.fit, X, y * 0)
```

### Step 15: Call pytest.raises()

```python
pytest.raises(TypeError, SPoC, cov_est='epoch')
```

### Step 16: Assign rs = np.random.RandomState(...)

```python
rs = np.random.RandomState(42)
```

### Step 17: Assign y = value

```python
y = rs.rand(100) * 50 + 1
```

### Step 18: Assign unknown = simulate_data(...)

```python
X, A = simulate_data(y)
```

### Step 19: Assign spoc = SPoC(...)

```python
spoc = SPoC(n_components=1)
```

### Step 20: Call spoc.fit()

```python
spoc.fit(X, y)
```

### Step 21: Assign corr = np.abs(...)

```python
corr = np.abs(np.corrcoef(spoc.patterns_[0, :].T, A[:, 0])[0, 1])
```

**Verification:**
```python
assert np.abs(corr) > 0.99
```

### Step 22: Assign out = spoc.transform(...)

```python
out = spoc.transform(X)
```

### Step 23: Assign corr = np.abs(...)

```python
corr = np.abs(np.corrcoef(out[:, 0], y)[0, 1])
```

**Verification:**
```python
assert np.abs(corr) > 0.85
```


## Complete Example

```python
# Workflow
'Test SPoC.'
X = np.random.randn(10, 10, 20)
y = np.random.randn(10)
spoc = SPoC(n_components=4)
spoc.fit(X, y)
Xt = spoc.transform(X)
assert_array_equal(Xt.shape, [10, 4])
spoc = SPoC(n_components=4, transform_into='csp_space')
spoc.fit(X, y)
Xt = spoc.transform(X)
assert_array_equal(Xt.shape, [10, 4, 20])
assert_array_equal(spoc.filters_.shape, [10, 10])
assert_array_equal(spoc.patterns_.shape, [10, 10])
pytest.raises(ValueError, spoc.fit, X, y * 0)
pytest.raises(TypeError, SPoC, cov_est='epoch')
rs = np.random.RandomState(42)
y = rs.rand(100) * 50 + 1
X, A = simulate_data(y)
spoc = SPoC(n_components=1)
spoc.fit(X, y)
corr = np.abs(np.corrcoef(spoc.patterns_[0, :].T, A[:, 0])[0, 1])
assert np.abs(corr) > 0.99
out = spoc.transform(X)
corr = np.abs(np.corrcoef(out[:, 0], y)[0, 1])
assert np.abs(corr) > 0.85
```

## Next Steps


---

*Source: test_csp.py:419 | Complexity: Advanced | Last updated: 2026-05-18*