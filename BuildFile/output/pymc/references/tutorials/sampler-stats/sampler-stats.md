# How To: Sampler Stats

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test sampler stats

## Prerequisites

**Required Modules:**
- `logging`
- `warnings`
- `numpy`
- `pytensor.tensor`
- `pytest`
- `pymc`
- `pymc.exceptions`
- `pymc.pytensorf`
- `pymc.step_methods.hmc`
- `tests`
- `tests.helpers`


## Step-by-Step Guide

### Step 1: Assign expected_stat_names = value

```python
expected_stat_names = {'depth', 'diverging', 'divergences', 'energy', 'energy_error', 'model_logp', 'max_energy_error', 'mean_tree_accept', 'step_size', 'step_size_bar', 'tree_size', 'perf_counter_diff', 'perf_counter_start', 'process_time_diff', 'reached_max_treedepth', 'index_in_trajectory', 'largest_eigval', 'smallest_eigval', 'warning'}
```

**Verification:**
```python
assert trace.stat_names == expected_stat_names
```

### Step 2: Assign model_logp_fn = model.compile_logp(...)

```python
model_logp_fn = model.compile_logp()
```

**Verification:**
```python
assert trace.get_sampler_stats(varname).shape == (10,)
```

### Step 3: Assign model_logp_ = np.array(...)

```python
model_logp_ = np.array([model_logp_fn(trace.point(i, chain=c)) for c in trace.chains for i in range(len(trace))])
```

**Verification:**
```python
assert (trace.model_logp == model_logp_).all()
```

### Step 4: Call pm.Normal()

```python
pm.Normal('x', mu=0, sigma=1)
```

**Verification:**
```python
assert trace.get_sampler_stats(varname).shape == (10,)
```

### Step 5: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', '.*number of samples.*', UserWarning)
```

### Step 6: Assign trace = pm.sample(...)

```python
trace = pm.sample(draws=10, tune=1, chains=1, return_inferencedata=False)
```


## Complete Example

```python
# Workflow
with pm.Model() as model:
    pm.Normal('x', mu=0, sigma=1)
    with warnings.catch_warnings():
        warnings.filterwarnings('ignore', '.*number of samples.*', UserWarning)
        trace = pm.sample(draws=10, tune=1, chains=1, return_inferencedata=False)
expected_stat_names = {'depth', 'diverging', 'divergences', 'energy', 'energy_error', 'model_logp', 'max_energy_error', 'mean_tree_accept', 'step_size', 'step_size_bar', 'tree_size', 'perf_counter_diff', 'perf_counter_start', 'process_time_diff', 'reached_max_treedepth', 'index_in_trajectory', 'largest_eigval', 'smallest_eigval', 'warning'}
assert trace.stat_names == expected_stat_names
for varname in trace.stat_names:
    if varname == 'warning':
        continue
    assert trace.get_sampler_stats(varname).shape == (10,)
model_logp_fn = model.compile_logp()
model_logp_ = np.array([model_logp_fn(trace.point(i, chain=c)) for c in trace.chains for i in range(len(trace))])
assert (trace.model_logp == model_logp_).all()
```

## Next Steps


---

*Source: test_nuts.py:143 | Complexity: Intermediate | Last updated: 2026-05-18*