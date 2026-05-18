# How To: List Mvnormals Predictive Sampling Shape

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test list mvnormals predictive sampling shape

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

### Step 1: Assign N = 100

```python
N = 100
```

**Verification:**
```python
assert ppc['x_obs'].shape == (1, n_samples, *X.shape)
```

### Step 2: Assign K = 3

```python
K = 3
```

**Verification:**
```python
assert prior['x_obs'].shape == (n_samples, *X.shape)
```

### Step 3: Assign D = 3

```python
D = 3
```

**Verification:**
```python
assert prior['mu0'].shape == (n_samples, D)
```

### Step 4: Assign X = MvNormal.dist.eval(...)

```python
X = MvNormal.dist(np.zeros(D), np.eye(D), size=N).eval()
```

**Verification:**
```python
assert prior['chol_cov_0'].shape == (n_samples, D * (D + 1) // 2)
```

### Step 5: Assign n_samples = 20

```python
n_samples = 20
```

**Verification:**
```python
assert ppc['x_obs'].shape == (1, n_samples, *X.shape)
```

### Step 6: Assign pi = Dirichlet(...)

```python
pi = Dirichlet('pi', np.ones(K), shape=(K,))
```

### Step 7: Assign comp_dist = value

```python
comp_dist = []
```

### Step 8: Assign mu = value

```python
mu = []
```

### Step 9: Assign packed_chol = value

```python
packed_chol = []
```

### Step 10: Assign chol = value

```python
chol = []
```

### Step 11: Call Mixture()

```python
Mixture('x_obs', pi, comp_dist, observed=X)
```

### Step 12: Assign prior = sample_prior_predictive(...)

```python
prior = sample_prior_predictive(draws=n_samples, return_inferencedata=False)
```

### Step 13: Assign ppc = sample_posterior_predictive(...)

```python
ppc = sample_posterior_predictive(n_samples * [self.get_initial_point(model)], return_inferencedata=False)
```

### Step 14: Call mu.append()

```python
mu.append(Normal(f'mu{i}', 0, 10, shape=D))
```

### Step 15: Call packed_chol.append()

```python
packed_chol.append(LKJCholeskyCov(f'chol_cov_{i}', eta=2, n=D, sd_dist=HalfNormal.dist(2.5, size=D), compute_corr=False))
```

### Step 16: Call chol.append()

```python
chol.append(expand_packed_triangular(D, packed_chol[i], lower=True))
```

### Step 17: Call comp_dist.append()

```python
comp_dist.append(MvNormal.dist(mu=mu[i], chol=chol[i], shape=D))
```


## Complete Example

```python
# Workflow
N = 100
K = 3
D = 3
X = MvNormal.dist(np.zeros(D), np.eye(D), size=N).eval()
with Model() as model:
    pi = Dirichlet('pi', np.ones(K), shape=(K,))
    comp_dist = []
    mu = []
    packed_chol = []
    chol = []
    for i in range(K):
        mu.append(Normal(f'mu{i}', 0, 10, shape=D))
        packed_chol.append(LKJCholeskyCov(f'chol_cov_{i}', eta=2, n=D, sd_dist=HalfNormal.dist(2.5, size=D), compute_corr=False))
        chol.append(expand_packed_triangular(D, packed_chol[i], lower=True))
        comp_dist.append(MvNormal.dist(mu=mu[i], chol=chol[i], shape=D))
    Mixture('x_obs', pi, comp_dist, observed=X)
n_samples = 20
with model:
    prior = sample_prior_predictive(draws=n_samples, return_inferencedata=False)
    ppc = sample_posterior_predictive(n_samples * [self.get_initial_point(model)], return_inferencedata=False)
assert ppc['x_obs'].shape == (1, n_samples, *X.shape)
assert prior['x_obs'].shape == (n_samples, *X.shape)
assert prior['mu0'].shape == (n_samples, D)
assert prior['chol_cov_0'].shape == (n_samples, D * (D + 1) // 2)
```

## Next Steps


---

*Source: test_mixture.py:579 | Complexity: Advanced | Last updated: 2026-05-18*