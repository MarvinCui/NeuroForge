# How To: Censored Workflow

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test censored workflow

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `scipy`
- `pymc`
- `pymc`
- `pymc.distributions.shape_utils`

**Setup Required:**
```python
# Fixtures: censored
```

## Step-by-Step Guide

### Step 1: Assign rng = np.random.default_rng(...)

```python
rng = np.random.default_rng(1234)
```

**Verification:**
```python
assert (9 < prior_pred.prior_predictive.mean() < 10) == expected
```

### Step 2: Assign size = 500

```python
size = 500
```

**Verification:**
```python
assert (13 < posterior.posterior['mu'].mean() < 14) == expected
```

### Step 3: Assign true_mu = 13.0

```python
true_mu = 13.0
```

**Verification:**
```python
assert (4.5 < posterior.posterior['sigma'].mean() < 5.5) == expected
```

### Step 4: Assign true_sigma = 5.0

```python
true_sigma = 5.0
```

**Verification:**
```python
assert (12 < posterior_pred.posterior_predictive.mean() < 13) == expected
```

### Step 5: Assign low = 3.0

```python
low = 3.0
```

### Step 6: Assign high = 16.0

```python
high = 16.0
```

### Step 7: Assign data = rng.normal(...)

```python
data = rng.normal(true_mu, true_sigma, size)
```

### Step 8: Assign unknown = low

```python
data[data <= low] = low
```

### Step 9: Assign unknown = high

```python
data[data >= high] = high
```

### Step 10: Assign rng = 17092021

```python
rng = 17092021
```

### Step 11: Assign expected = value

```python
expected = True if censored else False
```

**Verification:**
```python
assert (9 < prior_pred.prior_predictive.mean() < 10) == expected
```

### Step 12: Assign mu = pm.Normal(...)

```python
mu = pm.Normal('mu', mu=(high - low) / 2 + low, sigma=(high - low) / 2.0, initval='support_point')
```

### Step 13: Assign sigma = pm.HalfNormal(...)

```python
sigma = pm.HalfNormal('sigma', sigma=(high - low) / 2.0, initval='support_point')
```

### Step 14: Assign observed = pm.Censored(...)

```python
observed = pm.Censored('observed', pm.Normal.dist(mu=mu, sigma=sigma), lower=low if censored else None, upper=high if censored else None, observed=data)
```

### Step 15: Assign prior_pred = pm.sample_prior_predictive(...)

```python
prior_pred = pm.sample_prior_predictive(random_seed=rng)
```

### Step 16: Assign posterior = pm.sample(...)

```python
posterior = pm.sample(tune=500, draws=500, random_seed=rng)
```

### Step 17: Assign posterior_pred = pm.sample_posterior_predictive(...)

```python
posterior_pred = pm.sample_posterior_predictive(posterior, random_seed=rng)
```


## Complete Example

```python
# Setup
# Fixtures: censored

# Workflow
rng = np.random.default_rng(1234)
size = 500
true_mu = 13.0
true_sigma = 5.0
low = 3.0
high = 16.0
data = rng.normal(true_mu, true_sigma, size)
data[data <= low] = low
data[data >= high] = high
rng = 17092021
with pm.Model() as m:
    mu = pm.Normal('mu', mu=(high - low) / 2 + low, sigma=(high - low) / 2.0, initval='support_point')
    sigma = pm.HalfNormal('sigma', sigma=(high - low) / 2.0, initval='support_point')
    observed = pm.Censored('observed', pm.Normal.dist(mu=mu, sigma=sigma), lower=low if censored else None, upper=high if censored else None, observed=data)
    prior_pred = pm.sample_prior_predictive(random_seed=rng)
    posterior = pm.sample(tune=500, draws=500, random_seed=rng)
    posterior_pred = pm.sample_posterior_predictive(posterior, random_seed=rng)
expected = True if censored else False
assert (9 < prior_pred.prior_predictive.mean() < 10) == expected
assert (13 < posterior.posterior['mu'].mean() < 14) == expected
assert (4.5 < posterior.posterior['sigma'].mean() < 5.5) == expected
assert (12 < posterior_pred.posterior_predictive.mean() < 13) == expected
```

## Next Steps


---

*Source: test_censored.py:27 | Complexity: Advanced | Last updated: 2026-05-18*