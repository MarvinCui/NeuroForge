# How To: List Normals Sampling

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test list normals sampling

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

### Step 1: Assign norm_w = np.array(...)

```python
norm_w = np.array([0.75, 0.25])
```

**Verification:**
```python
assert_allclose(np.sort(trace['w'].mean(axis=0)), np.sort(norm_w), rtol=0.1, atol=0.1)
```

### Step 2: Assign norm_mu = np.array(...)

```python
norm_mu = np.array([0.0, 5.0])
```

**Verification:**
```python
assert_allclose(np.sort(trace['mu'].mean(axis=0)), np.sort(norm_mu), rtol=0.1, atol=0.1)
```

### Step 3: Assign norm_sigma = np.ones_like(...)

```python
norm_sigma = np.ones_like(norm_mu)
```

### Step 4: Assign norm_x = generate_normal_mixture_data(...)

```python
norm_x = generate_normal_mixture_data(norm_w, norm_mu, norm_sigma, size=1000)
```

### Step 5: Call assert_allclose()

```python
assert_allclose(np.sort(trace['w'].mean(axis=0)), np.sort(norm_w), rtol=0.1, atol=0.1)
```

### Step 6: Call assert_allclose()

```python
assert_allclose(np.sort(trace['mu'].mean(axis=0)), np.sort(norm_mu), rtol=0.1, atol=0.1)
```

### Step 7: Assign w = Dirichlet(...)

```python
w = Dirichlet('w', floatX(np.ones_like(norm_w)), shape=norm_w.size)
```

### Step 8: Assign mu = Normal(...)

```python
mu = Normal('mu', 0.0, 10.0, shape=norm_w.size)
```

### Step 9: Assign tau = Gamma(...)

```python
tau = Gamma('tau', 1.0, 1.0, shape=norm_w.size)
```

### Step 10: Call Mixture()

```python
Mixture('x_obs', w, [Normal.dist(mu[0], tau=tau[0]), Normal.dist(mu[1], tau=tau[1])], observed=norm_x)
```

### Step 11: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', 'More chains .* than draws.*', UserWarning)
```

### Step 12: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', 'overflow encountered in exp', RuntimeWarning)
```

### Step 13: Assign trace = sample(...)

```python
trace = sample(5000, chains=1, step=Metropolis(), random_seed=645334, progressbar=False, return_inferencedata=False)
```


## Complete Example

```python
# Workflow
norm_w = np.array([0.75, 0.25])
norm_mu = np.array([0.0, 5.0])
norm_sigma = np.ones_like(norm_mu)
norm_x = generate_normal_mixture_data(norm_w, norm_mu, norm_sigma, size=1000)
with Model() as model:
    w = Dirichlet('w', floatX(np.ones_like(norm_w)), shape=norm_w.size)
    mu = Normal('mu', 0.0, 10.0, shape=norm_w.size)
    tau = Gamma('tau', 1.0, 1.0, shape=norm_w.size)
    Mixture('x_obs', w, [Normal.dist(mu[0], tau=tau[0]), Normal.dist(mu[1], tau=tau[1])], observed=norm_x)
    with warnings.catch_warnings():
        warnings.filterwarnings('ignore', 'More chains .* than draws.*', UserWarning)
        warnings.filterwarnings('ignore', 'overflow encountered in exp', RuntimeWarning)
        trace = sample(5000, chains=1, step=Metropolis(), random_seed=645334, progressbar=False, return_inferencedata=False)
assert_allclose(np.sort(trace['w'].mean(axis=0)), np.sort(norm_w), rtol=0.1, atol=0.1)
assert_allclose(np.sort(trace['mu'].mean(axis=0)), np.sort(norm_mu), rtol=0.1, atol=0.1)
```

## Next Steps


---

*Source: test_mixture.py:510 | Complexity: Advanced | Last updated: 2026-05-18*