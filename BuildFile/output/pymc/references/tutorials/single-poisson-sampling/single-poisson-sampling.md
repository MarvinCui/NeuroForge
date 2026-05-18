# How To: Single Poisson Sampling

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test single poisson sampling

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `pytensor`
- `pytest`
- `scipy.stats`
- `numpy.testing`
- `pytensor`
- `pytensor.tensor`
- `pytensor.tensor.random.op`
- `scipy.special`
- `pymc.distributions`
- `pymc.distributions.mixture`
- `pymc.distributions.shape_utils`
- `pymc.distributions.transforms`
- `pymc.logprob.basic`
- `pymc.logprob.transforms`
- `pymc.math`
- `pymc.model`
- `pymc.pytensorf`
- `pymc.sampling.forward`
- `pymc.sampling.mcmc`
- `pymc.step_methods`
- `pymc.testing`
- `pymc.vartypes`


## Step-by-Step Guide

### Step 1: Assign pois_w = np.array(...)

```python
pois_w = np.array([0.4, 0.6])
```

**Verification:**
```python
assert_allclose(np.sort(trace['w'].mean(axis=0)), np.sort(pois_w), rtol=0.1, atol=0.1)
```

### Step 2: Assign pois_mu = np.array(...)

```python
pois_mu = np.array([5.0, 20.0])
```

**Verification:**
```python
assert_allclose(np.sort(trace['mu'].mean(axis=0)), np.sort(pois_mu), rtol=0.1, atol=0.1)
```

### Step 3: Assign pois_x = generate_poisson_mixture_data(...)

```python
pois_x = generate_poisson_mixture_data(pois_w, pois_mu, size=1000)
```

### Step 4: Call assert_allclose()

```python
assert_allclose(np.sort(trace['w'].mean(axis=0)), np.sort(pois_w), rtol=0.1, atol=0.1)
```

### Step 5: Call assert_allclose()

```python
assert_allclose(np.sort(trace['mu'].mean(axis=0)), np.sort(pois_mu), rtol=0.1, atol=0.1)
```

### Step 6: Assign w = Dirichlet(...)

```python
w = Dirichlet('w', floatX(np.ones_like(pois_w)), shape=pois_w.shape)
```

### Step 7: Assign mu = Gamma(...)

```python
mu = Gamma('mu', 1.0, 1.0, shape=pois_w.size)
```

### Step 8: Call Mixture()

```python
Mixture('x_obs', w, Poisson.dist(mu), observed=pois_x)
```

### Step 9: Assign step = Metropolis(...)

```python
step = Metropolis()
```

### Step 10: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', 'More chains .* than draws.*', UserWarning)
```

### Step 11: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', 'overflow encountered in exp', RuntimeWarning)
```

### Step 12: Assign trace = sample(...)

```python
trace = sample(5000, step=step, random_seed=45354, progressbar=False, chains=1, return_inferencedata=False)
```


## Complete Example

```python
# Workflow
pois_w = np.array([0.4, 0.6])
pois_mu = np.array([5.0, 20.0])
pois_x = generate_poisson_mixture_data(pois_w, pois_mu, size=1000)
with Model() as model:
    w = Dirichlet('w', floatX(np.ones_like(pois_w)), shape=pois_w.shape)
    mu = Gamma('mu', 1.0, 1.0, shape=pois_w.size)
    Mixture('x_obs', w, Poisson.dist(mu), observed=pois_x)
    step = Metropolis()
    with warnings.catch_warnings():
        warnings.filterwarnings('ignore', 'More chains .* than draws.*', UserWarning)
        warnings.filterwarnings('ignore', 'overflow encountered in exp', RuntimeWarning)
        trace = sample(5000, step=step, random_seed=45354, progressbar=False, chains=1, return_inferencedata=False)
assert_allclose(np.sort(trace['w'].mean(axis=0)), np.sort(pois_w), rtol=0.1, atol=0.1)
assert_allclose(np.sort(trace['mu'].mean(axis=0)), np.sort(pois_mu), rtol=0.1, atol=0.1)
```

## Next Steps


---

*Source: test_mixture.py:461 | Complexity: Advanced | Last updated: 2026-05-18*