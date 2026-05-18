# How To: Weighted Covariance

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test weighted covariance

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `pytest`
- `scipy.sparse`
- `pymc`
- `pymc.pytensorf`
- `pymc.step_methods.hmc`

**Setup Required:**
```python
# Fixtures: ndim, seed
```

## Step-by-Step Guide

### Step 1: Call np.random.seed()

```python
np.random.seed(seed)
```

**Verification:**
```python
assert np.allclose(mu_est, mu_est0)
```

### Step 2: Assign L = np.random.randn(...)

```python
L = np.random.randn(ndim, ndim)
```

**Verification:**
```python
assert np.allclose(cov_est, cov_est0)
```

### Step 3: Assign unknown = 0.0

```python
L[np.triu_indices_from(L, 1)] = 0.0
```

**Verification:**
```python
assert np.allclose(mu_est2, mu_est0)
```

### Step 4: Assign unknown = np.exp(...)

```python
L[np.diag_indices_from(L)] = np.exp(L[np.diag_indices_from(L)])
```

**Verification:**
```python
assert np.allclose(cov_est2, cov_est0)
```

### Step 5: Assign cov = np.dot(...)

```python
cov = np.dot(L, L.T)
```

### Step 6: Assign mean = np.random.randn(...)

```python
mean = np.random.randn(ndim)
```

### Step 7: Assign samples = np.random.multivariate_normal(...)

```python
samples = np.random.multivariate_normal(mean, cov, size=100)
```

### Step 8: Assign mu_est0 = np.mean(...)

```python
mu_est0 = np.mean(samples, axis=0)
```

### Step 9: Assign cov_est0 = np.cov(...)

```python
cov_est0 = np.cov(samples, rowvar=0)
```

### Step 10: Assign est = quadpotential._WeightedCovariance(...)

```python
est = quadpotential._WeightedCovariance(ndim)
```

### Step 11: Assign mu_est = est.current_mean(...)

```python
mu_est = est.current_mean()
```

### Step 12: Assign cov_est = est.current_covariance(...)

```python
cov_est = est.current_covariance()
```

**Verification:**
```python
assert np.allclose(mu_est, mu_est0)
```

### Step 13: Assign est2 = quadpotential._WeightedCovariance(...)

```python
est2 = quadpotential._WeightedCovariance(ndim, np.mean(samples[:10], axis=0), np.cov(samples[:10], rowvar=0, bias=True), 10)
```

### Step 14: Assign mu_est2 = est2.current_mean(...)

```python
mu_est2 = est2.current_mean()
```

### Step 15: Assign cov_est2 = est2.current_covariance(...)

```python
cov_est2 = est2.current_covariance()
```

**Verification:**
```python
assert np.allclose(mu_est2, mu_est0)
```

### Step 16: Call est.add_sample()

```python
est.add_sample(sample)
```

### Step 17: Call est2.add_sample()

```python
est2.add_sample(sample)
```


## Complete Example

```python
# Setup
# Fixtures: ndim, seed

# Workflow
np.random.seed(seed)
L = np.random.randn(ndim, ndim)
L[np.triu_indices_from(L, 1)] = 0.0
L[np.diag_indices_from(L)] = np.exp(L[np.diag_indices_from(L)])
cov = np.dot(L, L.T)
mean = np.random.randn(ndim)
samples = np.random.multivariate_normal(mean, cov, size=100)
mu_est0 = np.mean(samples, axis=0)
cov_est0 = np.cov(samples, rowvar=0)
est = quadpotential._WeightedCovariance(ndim)
for sample in samples:
    est.add_sample(sample)
mu_est = est.current_mean()
cov_est = est.current_covariance()
assert np.allclose(mu_est, mu_est0)
assert np.allclose(cov_est, cov_est0)
est2 = quadpotential._WeightedCovariance(ndim, np.mean(samples[:10], axis=0), np.cov(samples[:10], rowvar=0, bias=True), 10)
for sample in samples[10:]:
    est2.add_sample(sample)
mu_est2 = est2.current_mean()
cov_est2 = est2.current_covariance()
assert np.allclose(mu_est2, mu_est0)
assert np.allclose(cov_est2, cov_est0)
```

## Next Steps


---

*Source: test_quadpotential.py:160 | Complexity: Advanced | Last updated: 2026-05-18*