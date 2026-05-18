# How To: Compute Deterministics

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test compute deterministics

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `pymc.distributions`
- `pymc.model.core`
- `pymc.sampling.deterministic`
- `pymc.sampling.forward`
- `pymc`

**Setup Required:**
```python
# Fixtures: via
```

## Step-by-Step Guide

### Step 1: Assign dataset = value

```python
dataset = sample_prior_predictive(draws=5, model=m, var_names=['mu_raw', 'sigma_raw'], random_seed=22).prior
```

**Verification:**
```python
assert set(all_dets.data_vars.variables) == {'mu', 'sigma'}
```

### Step 2: Call assert_allclose()

```python
assert_allclose(all_dets['mu'], dataset['mu_raw'].cumsum('group'))
```

**Verification:**
```python
assert all_dets['mu'].dims == ('chain', 'draw', 'group')
```

### Step 3: Call assert_allclose()

```python
assert_allclose(all_dets['sigma'], np.exp(dataset['sigma_raw']))
```

**Verification:**
```python
assert all_dets['sigma'].dims == ('chain', 'draw')
```

### Step 4: Assign mode_kwargs = value

```python
mode_kwargs = {'compile_kwargs': {'mode': 'FAST_COMPILE'}} if via == 'compile_kwargs' else {'backend': 'FAST_COMPILE'}
```

**Verification:**
```python
assert_allclose(all_dets['mu'], dataset['mu_raw'].cumsum('group'))
```

### Step 5: Assign extended_with_mu = compute_deterministics(...)

```python
extended_with_mu = compute_deterministics(dataset, var_names=['mu'], merge_dataset=True, model=m, progressbar=False, **mode_kwargs)
```

**Verification:**
```python
assert_allclose(all_dets['sigma'], np.exp(dataset['sigma_raw']))
```

### Step 6: Call assert_allclose()

```python
assert_allclose(extended_with_mu['mu'], dataset['mu_raw'].cumsum('group'))
```

**Verification:**
```python
assert set(extended_with_mu.data_vars.variables) == {'mu_raw', 'sigma_raw', 'mu'}
```

### Step 7: Assign only_sigma = compute_deterministics(...)

```python
only_sigma = compute_deterministics(dataset, var_names=['sigma'], model=m, progressbar=False)
```

**Verification:**
```python
assert extended_with_mu['mu'].dims == ('chain', 'draw', 'group')
```

### Step 8: Call assert_allclose()

```python
assert_allclose(only_sigma['sigma'], np.exp(dataset['sigma_raw']))
```

**Verification:**
```python
assert_allclose(extended_with_mu['mu'], dataset['mu_raw'].cumsum('group'))
```

### Step 9: Assign mu_raw = Normal(...)

```python
mu_raw = Normal('mu_raw', 0, 1, dims='group')
```

**Verification:**
```python
assert set(only_sigma.data_vars.variables) == {'sigma'}
```

### Step 10: Assign mu = Deterministic(...)

```python
mu = Deterministic('mu', mu_raw.cumsum(), dims='group')
```

**Verification:**
```python
assert only_sigma['sigma'].dims == ('chain', 'draw')
```

### Step 11: Assign sigma_raw = Normal(...)

```python
sigma_raw = Normal('sigma_raw', 0, 1)
```

**Verification:**
```python
assert_allclose(only_sigma['sigma'], np.exp(dataset['sigma_raw']))
```

### Step 12: Assign sigma = Deterministic(...)

```python
sigma = Deterministic('sigma', sigma_raw.exp())
```

### Step 13: Assign all_dets = compute_deterministics(...)

```python
all_dets = compute_deterministics(dataset)
```


## Complete Example

```python
# Setup
# Fixtures: via

# Workflow
with Model(coords={'group': (0, 2, 4)}) as m:
    mu_raw = Normal('mu_raw', 0, 1, dims='group')
    mu = Deterministic('mu', mu_raw.cumsum(), dims='group')
    sigma_raw = Normal('sigma_raw', 0, 1)
    sigma = Deterministic('sigma', sigma_raw.exp())
dataset = sample_prior_predictive(draws=5, model=m, var_names=['mu_raw', 'sigma_raw'], random_seed=22).prior
with m:
    all_dets = compute_deterministics(dataset)
assert set(all_dets.data_vars.variables) == {'mu', 'sigma'}
assert all_dets['mu'].dims == ('chain', 'draw', 'group')
assert all_dets['sigma'].dims == ('chain', 'draw')
assert_allclose(all_dets['mu'], dataset['mu_raw'].cumsum('group'))
assert_allclose(all_dets['sigma'], np.exp(dataset['sigma_raw']))
mode_kwargs = {'compile_kwargs': {'mode': 'FAST_COMPILE'}} if via == 'compile_kwargs' else {'backend': 'FAST_COMPILE'}
extended_with_mu = compute_deterministics(dataset, var_names=['mu'], merge_dataset=True, model=m, progressbar=False, **mode_kwargs)
assert set(extended_with_mu.data_vars.variables) == {'mu_raw', 'sigma_raw', 'mu'}
assert extended_with_mu['mu'].dims == ('chain', 'draw', 'group')
assert_allclose(extended_with_mu['mu'], dataset['mu_raw'].cumsum('group'))
only_sigma = compute_deterministics(dataset, var_names=['sigma'], model=m, progressbar=False)
assert set(only_sigma.data_vars.variables) == {'sigma'}
assert only_sigma['sigma'].dims == ('chain', 'draw')
assert_allclose(only_sigma['sigma'], np.exp(dataset['sigma_raw']))
```

## Next Steps


---

*Source: test_deterministic.py:29 | Complexity: Advanced | Last updated: 2026-05-18*