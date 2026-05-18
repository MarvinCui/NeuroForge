# How To: Auto Low Rank

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test probabilistic low rank estimators.

## Prerequisites

**Required Modules:**
- `itertools`
- `sys`
- `inspect`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.pick`
- `mne.channels`
- `mne.cov`
- `mne.datasets`
- `mne.fixes`
- `mne.io`
- `mne.preprocessing`
- `mne.rank`
- `mne.utils`
- `sklearn`


## Step-by-Step Guide

### Step 1: 'Test probabilistic low rank estimators.'

```python
'Test probabilistic low rank estimators.'
```

**Verification:**
```python
assert_equal(info['best'], rank)
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('sklearn')
```

### Step 3: Assign unknown = value

```python
n_samples, n_features, rank = (400, 10, 5)
```

### Step 4: Assign sigma = 0.1

```python
sigma = 0.1
```

### Step 5: Assign X = get_data(...)

```python
X = get_data(n_samples=n_samples, n_features=n_features, rank=rank, sigma=sigma)
```

### Step 6: Assign method_params = value

```python
method_params = {'iter_n_components': [4, 5, 6]}
```

### Step 7: Assign cv = 3

```python
cv = 3
```

### Step 8: Assign n_jobs = 1

```python
n_jobs = 1
```

### Step 9: Assign mode = 'factor_analysis'

```python
mode = 'factor_analysis'
```

### Step 10: Assign rescale = 100000000.0

```python
rescale = 100000000.0
```

### Step 11: Assign unknown = _auto_low_rank_model(...)

```python
est, info = _auto_low_rank_model(X, mode=mode, n_jobs=n_jobs, method_params=method_params, cv=cv)
```

### Step 12: Call assert_equal()

```python
assert_equal(info['best'], rank)
```

### Step 13: Assign X = get_data(...)

```python
X = get_data(n_samples=n_samples, n_features=n_features, rank=rank, sigma=sigma)
```

### Step 14: Assign method_params = value

```python
method_params = {'iter_n_components': [n_features + 5]}
```

### Step 15: Assign msg = value

```python
msg = f'You are trying to estimate {n_features + 5} components on matrix with {n_features} features.'
```

### Step 16: Assign rng = np.random.RandomState(...)

```python
rng = np.random.RandomState(42)
```

### Step 17: Assign W = rng.randn(...)

```python
W = rng.randn(n_features, n_features)
```

### Step 18: Assign X = rng.randn(...)

```python
X = rng.randn(n_samples, rank)
```

### Step 19: Assign unknown = _safe_svd(...)

```python
U, _, _ = _safe_svd(W.copy())
```

### Step 20: Assign X = np.dot(...)

```python
X = np.dot(X, U[:, :rank].T)
```

### Step 21: Assign sigmas = value

```python
sigmas = sigma * rng.rand(n_features) + sigma / 2.0
```

### Step 22: Call _auto_low_rank_model()

```python
_auto_low_rank_model(X, mode=mode, n_jobs=n_jobs, method_params=method_params, cv=cv)
```


## Complete Example

```python
# Workflow
'Test probabilistic low rank estimators.'
pytest.importorskip('sklearn')
n_samples, n_features, rank = (400, 10, 5)
sigma = 0.1

def get_data(n_samples, n_features, rank, sigma):
    rng = np.random.RandomState(42)
    W = rng.randn(n_features, n_features)
    X = rng.randn(n_samples, rank)
    U, _, _ = _safe_svd(W.copy())
    X = np.dot(X, U[:, :rank].T)
    sigmas = sigma * rng.rand(n_features) + sigma / 2.0
    X += rng.randn(n_samples, n_features) * sigmas
    return X
X = get_data(n_samples=n_samples, n_features=n_features, rank=rank, sigma=sigma)
method_params = {'iter_n_components': [4, 5, 6]}
cv = 3
n_jobs = 1
mode = 'factor_analysis'
rescale = 100000000.0
X *= rescale
est, info = _auto_low_rank_model(X, mode=mode, n_jobs=n_jobs, method_params=method_params, cv=cv)
assert_equal(info['best'], rank)
X = get_data(n_samples=n_samples, n_features=n_features, rank=rank, sigma=sigma)
method_params = {'iter_n_components': [n_features + 5]}
msg = f'You are trying to estimate {n_features + 5} components on matrix with {n_features} features.'
with pytest.warns(RuntimeWarning, match=msg):
    _auto_low_rank_model(X, mode=mode, n_jobs=n_jobs, method_params=method_params, cv=cv)
```

## Next Steps


---

*Source: test_cov.py:611 | Complexity: Advanced | Last updated: 2026-05-18*