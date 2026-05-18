# How To: Conditional

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Compare HSGP conditional to unapproximated GP prior, pm.gp.Latent.  Draw samples from the
prior and compare them using MMD two sample test.  Tests both centered and non-centered
parametrization.  The conditional should match the prior when no data is observed.

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
# Fixtures: model, cov_func, X1, parametrization
```

## Step-by-Step Guide

### Step 1: 'Compare HSGP conditional to unapproximated GP prior, pm.gp.Latent.  Draw samples from the\n        prior and compare them using MMD two sample test.  Tests both centered and non-centered\n        parametrization.  The conditional should match the prior when no data is observed.\n        '

```python
'Compare HSGP conditional to unapproximated GP prior, pm.gp.Latent.  Draw samples from the\n        prior and compare them using MMD two sample test.  Tests both centered and non-centered\n        parametrization.  The conditional should match the prior when no data is observed.\n        '
```

**Verification:**
```python
assert not reject, 'H0 was rejected, even though HSGP prior and conditional should match.'
```

### Step 2: Assign samples1 = value

```python
samples1 = az.extract(idata.prior['f']).values.T
```

### Step 3: Assign samples2 = value

```python
samples2 = az.extract(idata.prior['fc']).values.T
```

### Step 4: Assign unknown = two_sample_test(...)

```python
h0, mmd, critical_value, reject = two_sample_test(samples1, samples2, n_sims=500, alpha=0.01)
```

**Verification:**
```python
assert not reject, 'H0 was rejected, even though HSGP prior and conditional should match.'
```

### Step 5: Assign hsgp = pm.gp.HSGP(...)

```python
hsgp = pm.gp.HSGP(m=[100], c=2.0, parametrization=parametrization, cov_func=cov_func)
```

### Step 6: Assign f = hsgp.prior(...)

```python
f = hsgp.prior('f', X=X1)
```

### Step 7: Assign fc = hsgp.conditional(...)

```python
fc = hsgp.conditional('fc', Xnew=X1)
```

### Step 8: Assign idata = pm.sample_prior_predictive(...)

```python
idata = pm.sample_prior_predictive(draws=1000)
```


## Complete Example

```python
# Setup
# Fixtures: model, cov_func, X1, parametrization

# Workflow
'Compare HSGP conditional to unapproximated GP prior, pm.gp.Latent.  Draw samples from the\n        prior and compare them using MMD two sample test.  Tests both centered and non-centered\n        parametrization.  The conditional should match the prior when no data is observed.\n        '
with model:
    hsgp = pm.gp.HSGP(m=[100], c=2.0, parametrization=parametrization, cov_func=cov_func)
    f = hsgp.prior('f', X=X1)
    fc = hsgp.conditional('fc', Xnew=X1)
    idata = pm.sample_prior_predictive(draws=1000)
samples1 = az.extract(idata.prior['f']).values.T
samples2 = az.extract(idata.prior['fc']).values.T
h0, mmd, critical_value, reject = two_sample_test(samples1, samples2, n_sims=500, alpha=0.01)
assert not reject, 'H0 was rejected, even though HSGP prior and conditional should match.'
```

## Next Steps


---

*Source: test_hsgp_approx.py:233 | Complexity: Advanced | Last updated: 2026-05-18*