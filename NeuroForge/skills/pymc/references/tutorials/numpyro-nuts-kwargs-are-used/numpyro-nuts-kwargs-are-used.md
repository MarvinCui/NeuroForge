# How To: Numpyro Nuts Kwargs Are Used

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: unittest, mock, workflow, integration

## Overview

Workflow: test numpyro nuts kwargs are used

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `logging`
- `re`
- `warnings`
- `collections.abc`
- `typing`
- `unittest`
- `jax`
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `xarray`
- `pytensor.compile`
- `pytensor.graph`
- `pymc`
- `pymc.exceptions`
- `pymc.sampling.jax`

**Setup Required:**
```python
# Fixtures: mocked
```

## Step-by-Step Guide

### Step 1: Assign mocked.side_effect = MCMC

```python
mocked.side_effect = MCMC
```

**Verification:**
```python
assert nuts_sampler._step_size == step_size
```

### Step 2: Assign step_size = 0.13

```python
step_size = 0.13
```

**Verification:**
```python
assert nuts_sampler._dense_mass == dense_mass
```

### Step 3: Assign dense_mass = True

```python
dense_mass = True
```

**Verification:**
```python
assert nuts_sampler._adapt_step_size == adapt_step_size
```

### Step 4: Assign adapt_step_size = False

```python
adapt_step_size = False
```

**Verification:**
```python
assert nuts_sampler._adapt_mass_matrix
```

### Step 5: Assign target_accept = 0.78

```python
target_accept = 0.78
```

**Verification:**
```python
assert nuts_sampler._target_accept_prob == target_accept
```

### Step 6: Call mocked.assert_called_once()

```python
mocked.assert_called_once()
```

### Step 7: Assign nuts_sampler = value

```python
nuts_sampler = mocked.call_args.args[0]
```

**Verification:**
```python
assert nuts_sampler._step_size == step_size
```

### Step 8: Call pm.Normal()

```python
pm.Normal('a')
```

### Step 9: Call sample_numpyro_nuts()

```python
sample_numpyro_nuts(10, tune=10, chains=1, target_accept=target_accept, nuts_kwargs={'step_size': step_size, 'dense_mass': dense_mass, 'adapt_step_size': adapt_step_size})
```


## Complete Example

```python
# Setup
# Fixtures: mocked

# Workflow
mocked.side_effect = MCMC
step_size = 0.13
dense_mass = True
adapt_step_size = False
target_accept = 0.78
with pm.Model():
    pm.Normal('a')
    sample_numpyro_nuts(10, tune=10, chains=1, target_accept=target_accept, nuts_kwargs={'step_size': step_size, 'dense_mass': dense_mass, 'adapt_step_size': adapt_step_size})
mocked.assert_called_once()
nuts_sampler = mocked.call_args.args[0]
assert nuts_sampler._step_size == step_size
assert nuts_sampler._dense_mass == dense_mass
assert nuts_sampler._adapt_step_size == adapt_step_size
assert nuts_sampler._adapt_mass_matrix
assert nuts_sampler._target_accept_prob == target_accept
```

## Next Steps


---

*Source: test_jax.py:394 | Complexity: Advanced | Last updated: 2026-05-18*