# How To: Single Poisson Predictive Sampling Shape

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test single poisson predictive sampling shape

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

### Step 1: Assign rng = self.get_random_state(...)

```python
rng = self.get_random_state()
```

**Verification:**
```python
assert prior['like0'].shape == (n_samples, 20)
```

### Step 2: Assign y = np.concatenate(...)

```python
y = np.concatenate([rng.poisson(5, size=10), rng.poisson(9, size=10)])
```

**Verification:**
```python
assert prior['like1'].shape == (n_samples, 20)
```

### Step 3: Assign n_samples = 30

```python
n_samples = 30
```

**Verification:**
```python
assert prior['like2'].shape == (n_samples, 20)
```

### Step 4: Assign comp0 = Poisson.dist(...)

```python
comp0 = Poisson.dist(mu=np.ones(2))
```

**Verification:**
```python
assert prior['like3'].shape == (n_samples, 20)
```

### Step 5: Assign w0 = Dirichlet(...)

```python
w0 = Dirichlet('w0', a=np.ones(2), shape=(2,))
```

**Verification:**
```python
assert ppc['like0'].shape == (1, n_samples, 20)
```

### Step 6: Assign like0 = Mixture(...)

```python
like0 = Mixture('like0', w=w0, comp_dists=comp0, observed=y)
```

**Verification:**
```python
assert ppc['like1'].shape == (1, n_samples, 20)
```

### Step 7: Assign comp1 = Poisson.dist(...)

```python
comp1 = Poisson.dist(mu=np.ones((20, 2)), shape=(20, 2))
```

**Verification:**
```python
assert ppc['like2'].shape == (1, n_samples, 20)
```

### Step 8: Assign w1 = Dirichlet(...)

```python
w1 = Dirichlet('w1', a=np.ones(2), shape=(2,))
```

**Verification:**
```python
assert ppc['like3'].shape == (1, n_samples, 20)
```

### Step 9: Assign like1 = Mixture(...)

```python
like1 = Mixture('like1', w=w1, comp_dists=comp1, observed=y)
```

### Step 10: Assign comp2 = Poisson.dist(...)

```python
comp2 = Poisson.dist(mu=np.ones(2))
```

### Step 11: Assign w2 = Dirichlet(...)

```python
w2 = Dirichlet('w2', a=np.ones(2), shape=(20, 2))
```

### Step 12: Assign like2 = Mixture(...)

```python
like2 = Mixture('like2', w=w2, comp_dists=comp2, observed=y)
```

### Step 13: Assign comp3 = Poisson.dist(...)

```python
comp3 = Poisson.dist(mu=np.ones(2), shape=(20, 2))
```

### Step 14: Assign w3 = Dirichlet(...)

```python
w3 = Dirichlet('w3', a=np.ones(2), shape=(20, 2))
```

### Step 15: Assign like3 = Mixture(...)

```python
like3 = Mixture('like3', w=w3, comp_dists=comp3, observed=y)
```

### Step 16: Assign prior = sample_prior_predictive(...)

```python
prior = sample_prior_predictive(draws=n_samples, return_inferencedata=False)
```

### Step 17: Assign ppc = sample_posterior_predictive(...)

```python
ppc = sample_posterior_predictive(n_samples * [self.get_initial_point(model)], return_inferencedata=False)
```


## Complete Example

```python
# Workflow
rng = self.get_random_state()
y = np.concatenate([rng.poisson(5, size=10), rng.poisson(9, size=10)])
with Model() as model:
    comp0 = Poisson.dist(mu=np.ones(2))
    w0 = Dirichlet('w0', a=np.ones(2), shape=(2,))
    like0 = Mixture('like0', w=w0, comp_dists=comp0, observed=y)
    comp1 = Poisson.dist(mu=np.ones((20, 2)), shape=(20, 2))
    w1 = Dirichlet('w1', a=np.ones(2), shape=(2,))
    like1 = Mixture('like1', w=w1, comp_dists=comp1, observed=y)
    comp2 = Poisson.dist(mu=np.ones(2))
    w2 = Dirichlet('w2', a=np.ones(2), shape=(20, 2))
    like2 = Mixture('like2', w=w2, comp_dists=comp2, observed=y)
    comp3 = Poisson.dist(mu=np.ones(2), shape=(20, 2))
    w3 = Dirichlet('w3', a=np.ones(2), shape=(20, 2))
    like3 = Mixture('like3', w=w3, comp_dists=comp3, observed=y)
n_samples = 30
with model:
    prior = sample_prior_predictive(draws=n_samples, return_inferencedata=False)
    ppc = sample_posterior_predictive(n_samples * [self.get_initial_point(model)], return_inferencedata=False)
assert prior['like0'].shape == (n_samples, 20)
assert prior['like1'].shape == (n_samples, 20)
assert prior['like2'].shape == (n_samples, 20)
assert prior['like3'].shape == (n_samples, 20)
assert ppc['like0'].shape == (1, n_samples, 20)
assert ppc['like1'].shape == (1, n_samples, 20)
assert ppc['like2'].shape == (1, n_samples, 20)
assert ppc['like3'].shape == (1, n_samples, 20)
```

## Next Steps


---

*Source: test_mixture.py:541 | Complexity: Advanced | Last updated: 2026-05-18*