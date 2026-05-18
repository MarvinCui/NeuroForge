# How To: Sample Var Names

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test sample var names

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `logging`
- `unittest.mock`
- `warnings`
- `contextlib`
- `types`
- `numpy`
- `numpy.testing`
- `pytensor.tensor`
- `pytest`
- `xarray`
- `pymc`
- `pymc.exceptions`
- `pymc.progress_bar`
- `pymc.step_methods.hmc.quadpotential`

**Setup Required:**
```python
# Fixtures: nuts_sampler
```

## Step-by-Step Guide

### Step 1: Assign seed = 1234

```python
seed = 1234
```

**Verification:**
```python
assert 'mu' in idata_1.posterior
```

### Step 2: Assign kwargs = value

```python
kwargs = {'chains': 1, 'tune': 100, 'draws': 100, 'random_seed': seed, 'progressbar': False, 'compute_convergence_checks': False}
```

**Verification:**
```python
assert 'mu' not in idata_2.posterior
```

### Step 3: Assign rng = np.random.default_rng(...)

```python
rng = np.random.default_rng(seed)
```

**Verification:**
```python
assert free_RVs[-1] in idata_1.posterior
```

### Step 4: Assign group = rng.choice(...)

```python
group = rng.choice(list('ABCD'), size=100)
```

**Verification:**
```python
assert free_RVs[-1] not in idata_2.posterior
```

### Step 5: Assign x = rng.normal(...)

```python
x = rng.normal(size=100)
```

**Verification:**
```python
assert var in idata_1.posterior
```

### Step 6: Assign y = rng.normal(...)

```python
y = rng.normal(size=100)
```

**Verification:**
```python
assert var in idata_2.posterior
```

### Step 7: Assign unknown = np.unique(...)

```python
group_values, group_idx = np.unique(group, return_inverse=True)
```

### Step 8: Assign coords = value

```python
coords = {'group': group_values}
```

### Step 9: Assign free_RVs = value

```python
free_RVs = [var.name for var in model.free_RVs]
```

**Verification:**
```python
assert 'mu' in idata_1.posterior
```

### Step 10: Call pytest.importorskip()

```python
pytest.importorskip(nuts_sampler)
```

### Step 11: Assign b_group = Normal(...)

```python
b_group = Normal('b_group', dims='group')
```

### Step 12: Assign b_x = Normal(...)

```python
b_x = Normal('b_x')
```

### Step 13: Assign mu = Deterministic(...)

```python
mu = Deterministic('mu', b_group[group_idx] + b_x * x)
```

### Step 14: Assign sigma = HalfNormal(...)

```python
sigma = HalfNormal('sigma')
```

### Step 15: Call Normal()

```python
Normal('y', mu=mu, sigma=sigma, observed=y)
```

### Step 16: Assign idata_1 = sample(...)

```python
idata_1 = sample(nuts_sampler=nuts_sampler, **kwargs)
```

### Step 17: Assign idata_2 = sample(...)

```python
idata_2 = sample(nuts_sampler=nuts_sampler, var_names=free_RVs[:-1], **kwargs)
```

**Verification:**
```python
assert var in idata_1.posterior
```

### Step 18: Call xr.testing.assert_allclose()

```python
xr.testing.assert_allclose(idata_1.posterior[var], idata_2.posterior[var])
```


## Complete Example

```python
# Setup
# Fixtures: nuts_sampler

# Workflow
if nuts_sampler != 'pymc':
    pytest.importorskip(nuts_sampler)
seed = 1234
kwargs = {'chains': 1, 'tune': 100, 'draws': 100, 'random_seed': seed, 'progressbar': False, 'compute_convergence_checks': False}
rng = np.random.default_rng(seed)
group = rng.choice(list('ABCD'), size=100)
x = rng.normal(size=100)
y = rng.normal(size=100)
group_values, group_idx = np.unique(group, return_inverse=True)
coords = {'group': group_values}
with Model(coords=coords) as model:
    b_group = Normal('b_group', dims='group')
    b_x = Normal('b_x')
    mu = Deterministic('mu', b_group[group_idx] + b_x * x)
    sigma = HalfNormal('sigma')
    Normal('y', mu=mu, sigma=sigma, observed=y)
free_RVs = [var.name for var in model.free_RVs]
with model:
    idata_1 = sample(nuts_sampler=nuts_sampler, **kwargs)
    idata_2 = sample(nuts_sampler=nuts_sampler, var_names=free_RVs[:-1], **kwargs)
assert 'mu' in idata_1.posterior
assert 'mu' not in idata_2.posterior
assert free_RVs[-1] in idata_1.posterior
assert free_RVs[-1] not in idata_2.posterior
for var in free_RVs[:-1]:
    assert var in idata_1.posterior
    assert var in idata_2.posterior
    xr.testing.assert_allclose(idata_1.posterior[var], idata_2.posterior[var])
```

## Next Steps


---

*Source: test_mcmc_external.py:105 | Complexity: Advanced | Last updated: 2026-05-18*