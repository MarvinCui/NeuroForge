# How To: Split Warmup

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test split warmup

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
# Fixtures: tune, model, model_step, include_transformed
```

## Step-by-Step Guide

### Step 1: Assign store = zarr.MemoryStore(...)

```python
store = zarr.MemoryStore()
```

**Verification:**
```python
assert len(trace.root.posterior.draw) == draws
```

### Step 2: Assign trace = ZarrTrace(...)

```python
trace = ZarrTrace(store=store, include_transformed=include_transformed)
```

**Verification:**
```python
assert len(trace.root.sample_stats.draw) == draws
```

### Step 3: Assign draws = value

```python
draws = 10 - tune
```

**Verification:**
```python
assert len(trace.root['warmup_posterior'].draw) == tune
```

### Step 4: Call trace.init_trace()

```python
trace.init_trace(chains=1, draws=draws, tune=tune, model=model, step=model_step)
```

**Verification:**
```python
assert len(trace.root['warmup_sample_stats'].draw) == tune
```

### Step 5: Call trace.split_warmup()

```python
trace.split_warmup('posterior')
```

**Verification:**
```python
assert posterior_array.shape[1] == draws
```

### Step 6: Call trace.split_warmup()

```python
trace.split_warmup('sample_stats')
```

**Verification:**
```python
assert trace.root['warmup_posterior'][var_name].shape[1] == tune
```

### Step 7: trace.root['warmup_posterior']

```python
trace.root['warmup_posterior']
```

**Verification:**
```python
assert sample_stats_array.shape[1] == draws
```

### Step 8: Call trace.split_warmup()

```python
trace.split_warmup('posterior')
```

**Verification:**
```python
assert trace.root['warmup_sample_stats'][var_name].shape[1] == tune
```

### Step 9: Assign dims = value

```python
dims = posterior_array.attrs['_ARRAY_DIMENSIONS']
```

### Step 10: Assign dims = value

```python
dims = sample_stats_array.attrs['_ARRAY_DIMENSIONS']
```

**Verification:**
```python
assert posterior_array.shape[1] == draws
```


## Complete Example

```python
# Setup
# Fixtures: tune, model, model_step, include_transformed

# Workflow
store = zarr.MemoryStore()
trace = ZarrTrace(store=store, include_transformed=include_transformed)
draws = 10 - tune
trace.init_trace(chains=1, draws=draws, tune=tune, model=model, step=model_step)
trace.split_warmup('posterior')
trace.split_warmup('sample_stats')
assert len(trace.root.posterior.draw) == draws
assert len(trace.root.sample_stats.draw) == draws
if tune == 0:
    with pytest.raises(KeyError):
        trace.root['warmup_posterior']
else:
    assert len(trace.root['warmup_posterior'].draw) == tune
    assert len(trace.root['warmup_sample_stats'].draw) == tune
    with pytest.raises(RuntimeError):
        trace.split_warmup('posterior')
    for var_name, posterior_array in trace.posterior.arrays():
        dims = posterior_array.attrs['_ARRAY_DIMENSIONS']
        if len(dims) >= 2 and dims[1] == 'draw':
            assert posterior_array.shape[1] == draws
            assert trace.root['warmup_posterior'][var_name].shape[1] == tune
    for var_name, sample_stats_array in trace.sample_stats.arrays():
        dims = sample_stats_array.attrs['_ARRAY_DIMENSIONS']
        if len(dims) >= 2 and dims[1] == 'draw':
            assert sample_stats_array.shape[1] == draws
            assert trace.root['warmup_sample_stats'][var_name].shape[1] == tune
```

## Next Steps


---

*Source: test_zarr.py:342 | Complexity: Advanced | Last updated: 2026-05-18*