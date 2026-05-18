# How To: Gaussian Inference

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test gaussian inference

## Prerequisites

**Required Modules:**
- `numpy`
- `pytensor`
- `pytest`
- `scipy.stats`
- `pytensor.tensor.random.op`
- `pymc`
- `pymc`
- `pymc.distributions.continuous`
- `pymc.distributions.distribution`
- `pymc.distributions.multivariate`
- `pymc.distributions.shape_utils`
- `pymc.distributions.timeseries`
- `pymc.logprob.basic`
- `pymc.model`
- `pymc.pytensorf`
- `pymc.sampling.forward`
- `pymc.sampling.mcmc`
- `pymc.testing`


## Step-by-Step Guide

### Step 1: Assign unknown = value

```python
mu, sigma, steps = (2, 1, 1000)
```

### Step 2: Assign obs = np.concatenate.cumsum(...)

```python
obs = np.concatenate([[0], np.random.normal(mu, sigma, size=steps)]).cumsum()
```

### Step 3: Assign recovered_mu = unknown.mean(...)

```python
recovered_mu = trace.posterior['mu'].mean()
```

### Step 4: Assign recovered_sigma = unknown.mean(...)

```python
recovered_sigma = trace.posterior['sigma'].mean()
```

### Step 5: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose([mu, sigma], [recovered_mu, recovered_sigma], atol=0.2)
```

### Step 6: Assign _mu = Uniform(...)

```python
_mu = Uniform('mu', -10, 10)
```

### Step 7: Assign _sigma = Uniform(...)

```python
_sigma = Uniform('sigma', 0, 10)
```

### Step 8: Assign obs_data = Data(...)

```python
obs_data = Data('obs_data', obs)
```

### Step 9: Assign grw = GaussianRandomWalk(...)

```python
grw = GaussianRandomWalk('grw', _mu, _sigma, steps=steps, observed=obs_data, init_dist=Normal.dist(0, 100))
```

### Step 10: Assign trace = sample(...)

```python
trace = sample(chains=1)
```


## Complete Example

```python
# Workflow
mu, sigma, steps = (2, 1, 1000)
obs = np.concatenate([[0], np.random.normal(mu, sigma, size=steps)]).cumsum()
with Model():
    _mu = Uniform('mu', -10, 10)
    _sigma = Uniform('sigma', 0, 10)
    obs_data = Data('obs_data', obs)
    grw = GaussianRandomWalk('grw', _mu, _sigma, steps=steps, observed=obs_data, init_dist=Normal.dist(0, 100))
    trace = sample(chains=1)
recovered_mu = trace.posterior['mu'].mean()
recovered_sigma = trace.posterior['sigma'].mean()
np.testing.assert_allclose([mu, sigma], [recovered_mu, recovered_sigma], atol=0.2)
```

## Next Steps


---

*Source: test_timeseries.py:403 | Complexity: Advanced | Last updated: 2026-05-18*