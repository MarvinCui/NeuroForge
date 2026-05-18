# How To: Prior

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Compare HSGPPeriodic prior to unapproximated GP prior, pm.gp.Latent. Draw samples from the
prior and compare them using MMD two sample test.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `arviz`
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `scipy.spatial`
- `pymc`

**Setup Required:**
```python
# Fixtures: model, cov_func, eta, X1, rng
```

## Step-by-Step Guide

### Step 1: 'Compare HSGPPeriodic prior to unapproximated GP prior, pm.gp.Latent. Draw samples from the\n        prior and compare them using MMD two sample test.\n        '

```python
'Compare HSGPPeriodic prior to unapproximated GP prior, pm.gp.Latent. Draw samples from the\n        prior and compare them using MMD two sample test.\n        '
```

**Verification:**
```python
assert not reject, f'H0 was rejected, {mmd} even though HSGP and GP priors should match.'
```

### Step 2: Assign samples1 = value

```python
samples1 = az.extract(idata.prior['f1']).values.T
```

### Step 3: Assign samples2 = value

```python
samples2 = az.extract(idata.prior['f2']).values.T
```

### Step 4: Assign unknown = two_sample_test(...)

```python
h0, mmd, critical_value, reject = two_sample_test(samples1, samples2, n_sims=500, alpha=0.01)
```

**Verification:**
```python
assert not reject, f'H0 was rejected, {mmd} even though HSGP and GP priors should match.'
```

### Step 5: Assign hsgp = pm.gp.HSGPPeriodic(...)

```python
hsgp = pm.gp.HSGPPeriodic(m=200, scale=eta, cov_func=cov_func)
```

### Step 6: Assign f1 = hsgp.prior(...)

```python
f1 = hsgp.prior('f1', X=X1)
```

### Step 7: Assign gp = pm.gp.Latent(...)

```python
gp = pm.gp.Latent(cov_func=eta ** 2 * cov_func)
```

### Step 8: Assign f2 = gp.prior(...)

```python
f2 = gp.prior('f2', X=X1)
```

### Step 9: Assign idata = pm.sample_prior_predictive(...)

```python
idata = pm.sample_prior_predictive(draws=1000, random_seed=rng)
```


## Complete Example

```python
# Setup
# Fixtures: model, cov_func, eta, X1, rng

# Workflow
'Compare HSGPPeriodic prior to unapproximated GP prior, pm.gp.Latent. Draw samples from the\n        prior and compare them using MMD two sample test.\n        '
with model:
    hsgp = pm.gp.HSGPPeriodic(m=200, scale=eta, cov_func=cov_func)
    f1 = hsgp.prior('f1', X=X1)
    gp = pm.gp.Latent(cov_func=eta ** 2 * cov_func)
    f2 = gp.prior('f2', X=X1)
    idata = pm.sample_prior_predictive(draws=1000, random_seed=rng)
samples1 = az.extract(idata.prior['f1']).values.T
samples2 = az.extract(idata.prior['f2']).values.T
h0, mmd, critical_value, reject = two_sample_test(samples1, samples2, n_sims=500, alpha=0.01)
assert not reject, f'H0 was rejected, {mmd} even though HSGP and GP priors should match.'
```

## Next Steps


---

*Source: test_hsgp_approx.py:292 | Complexity: Advanced | Last updated: 2026-05-18*