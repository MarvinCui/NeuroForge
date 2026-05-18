# How To: Idata Contains Stats

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, unittest, workflow, integration

## Overview

Workflow: Tests whether sampler statistics were written to sample_stats
group of idata

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
# Fixtures: sampler_name
```

## Step-by-Step Guide

### Step 1: 'Tests whether sampler statistics were written to sample_stats\n    group of idata'

```python
'Tests whether sampler statistics were written to sample_stats\n    group of idata'
```

**Verification:**
```python
assert stats is not None
```

### Step 2: Assign stats = idata.get(...)

```python
stats = idata.get('sample_stats')
```

**Verification:**
```python
assert stat_var in stats.variables
```

### Step 3: Assign n_chains = value

```python
n_chains = stats.sizes['chain']
```

**Verification:**
```python
assert stats.get(stat_var).values.shape == stat_var_dims
```

### Step 4: Assign n_draws = value

```python
n_draws = stats.sizes['draw']
```

### Step 5: Assign expected_stat_vars = value

```python
expected_stat_vars = {'acceptance_rate': (n_chains, n_draws), 'diverging': (n_chains, n_draws), 'energy': (n_chains, n_draws), 'tree_depth': (n_chains, n_draws), 'lp': (n_chains, n_draws)}
```

### Step 6: Assign sampler = sample_blackjax_nuts

```python
sampler = sample_blackjax_nuts
```

### Step 7: Call pm.Normal()

```python
pm.Normal('a')
```

### Step 8: Assign idata = sampler(...)

```python
idata = sampler(tune=50, draws=50)
```

### Step 9: Assign blackjax_special_vars = value

```python
blackjax_special_vars = {}
```

### Step 10: Assign stat_vars = value

```python
stat_vars = expected_stat_vars | blackjax_special_vars
```

**Verification:**
```python
assert stat_var in stats.variables
```

### Step 11: Assign sampler = sample_numpyro_nuts

```python
sampler = sample_numpyro_nuts
```

### Step 12: Assign numpyro_special_vars = value

```python
numpyro_special_vars = {'step_size': (n_chains, n_draws), 'n_steps': (n_chains, n_draws)}
```

### Step 13: Assign stat_vars = value

```python
stat_vars = expected_stat_vars | numpyro_special_vars
```


## Complete Example

```python
# Setup
# Fixtures: sampler_name

# Workflow
'Tests whether sampler statistics were written to sample_stats\n    group of idata'
if sampler_name == 'sample_blackjax_nuts':
    sampler = sample_blackjax_nuts
elif sampler_name == 'sample_numpyro_nuts':
    sampler = sample_numpyro_nuts
with pm.Model():
    pm.Normal('a')
    idata = sampler(tune=50, draws=50)
stats = idata.get('sample_stats')
assert stats is not None
n_chains = stats.sizes['chain']
n_draws = stats.sizes['draw']
expected_stat_vars = {'acceptance_rate': (n_chains, n_draws), 'diverging': (n_chains, n_draws), 'energy': (n_chains, n_draws), 'tree_depth': (n_chains, n_draws), 'lp': (n_chains, n_draws)}
if sampler_name == 'sample_blackjax_nuts':
    blackjax_special_vars = {}
    stat_vars = expected_stat_vars | blackjax_special_vars
elif sampler_name == 'sample_numpyro_nuts':
    numpyro_special_vars = {'step_size': (n_chains, n_draws), 'n_steps': (n_chains, n_draws)}
    stat_vars = expected_stat_vars | numpyro_special_vars
for stat_var, stat_var_dims in stat_vars.items():
    assert stat_var in stats.variables
    assert stats.get(stat_var).values.shape == stat_var_dims
```

## Next Steps


---

*Source: test_jax.py:431 | Complexity: Advanced | Last updated: 2026-05-18*