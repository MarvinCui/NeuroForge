# How To: Sampling Consistency

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test sampling consistency

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `itertools`
- `dataclasses`
- `importlib.metadata`
- `numpy`
- `pytest`
- `xarray`
- `zarr`
- `pymc`
- `pymc.backends.zarr`
- `pymc.stats.convergence`
- `pymc.step_methods`
- `pymc.step_methods.state`
- `tests.helpers`

**Setup Required:**
```python
# Fixtures: model, model_step, draws_per_chunk
```

## Step-by-Step Guide

### Step 1: Assign store1 = zarr.TempStore(...)

```python
store1 = zarr.TempStore()
```

**Verification:**
```python
assert equal_sampling_states(parallel_trace._sampling_state.sampling_state[chain], sequential_trace._sampling_state.sampling_state[chain])
```

### Step 2: Assign parallel_trace = ZarrTrace(...)

```python
parallel_trace = ZarrTrace(store=store1, include_transformed=include_transformed, draws_per_chunk=draws_per_chunk)
```

### Step 3: Assign store2 = zarr.TempStore(...)

```python
store2 = zarr.TempStore()
```

### Step 4: Assign sequential_trace = ZarrTrace(...)

```python
sequential_trace = ZarrTrace(store=store2, include_transformed=include_transformed, draws_per_chunk=draws_per_chunk)
```

### Step 5: Assign tune = 2

```python
tune = 2
```

### Step 6: Assign draws = 3

```python
draws = 3
```

### Step 7: Assign chains = 2

```python
chains = 2
```

### Step 8: Assign random_seed = 12345

```python
random_seed = 12345
```

### Step 9: Assign initial_step_state = value

```python
initial_step_state = model_step.sampling_state
```

### Step 10: Call xr.testing.assert_equal()

```python
xr.testing.assert_equal(parallel_idata.posterior, sequential_idata.posterior)
```

### Step 11: Assign parallel_idata = pm.sample(...)

```python
parallel_idata = pm.sample(draws=draws, tune=tune, chains=chains, cores=chains, trace=parallel_trace, step=model_step, discard_tuned_samples=True, return_inferencedata=True, keep_warning_stat=False, idata_kwargs={'log_likelihood': False}, random_seed=random_seed)
```

### Step 12: Assign model_step.sampling_state = initial_step_state

```python
model_step.sampling_state = initial_step_state
```

### Step 13: Assign sequential_idata = pm.sample(...)

```python
sequential_idata = pm.sample(draws=draws, tune=tune, chains=chains, cores=1, trace=sequential_trace, step=model_step, discard_tuned_samples=True, return_inferencedata=True, keep_warning_stat=False, idata_kwargs={'log_likelihood': False}, random_seed=random_seed)
```

**Verification:**
```python
assert equal_sampling_states(parallel_trace._sampling_state.sampling_state[chain], sequential_trace._sampling_state.sampling_state[chain])
```


## Complete Example

```python
# Setup
# Fixtures: model, model_step, draws_per_chunk

# Workflow
store1 = zarr.TempStore()
parallel_trace = ZarrTrace(store=store1, include_transformed=include_transformed, draws_per_chunk=draws_per_chunk)
store2 = zarr.TempStore()
sequential_trace = ZarrTrace(store=store2, include_transformed=include_transformed, draws_per_chunk=draws_per_chunk)
tune = 2
draws = 3
chains = 2
random_seed = 12345
initial_step_state = model_step.sampling_state
with model:
    parallel_idata = pm.sample(draws=draws, tune=tune, chains=chains, cores=chains, trace=parallel_trace, step=model_step, discard_tuned_samples=True, return_inferencedata=True, keep_warning_stat=False, idata_kwargs={'log_likelihood': False}, random_seed=random_seed)
    model_step.sampling_state = initial_step_state
    sequential_idata = pm.sample(draws=draws, tune=tune, chains=chains, cores=1, trace=sequential_trace, step=model_step, discard_tuned_samples=True, return_inferencedata=True, keep_warning_stat=False, idata_kwargs={'log_likelihood': False}, random_seed=random_seed)
for chain in range(chains):
    assert equal_sampling_states(parallel_trace._sampling_state.sampling_state[chain], sequential_trace._sampling_state.sampling_state[chain])
xr.testing.assert_equal(parallel_idata.posterior, sequential_idata.posterior)
```

## Next Steps


---

*Source: test_zarr.py:500 | Complexity: Advanced | Last updated: 2026-05-18*