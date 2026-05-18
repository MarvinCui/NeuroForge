# How To: Compilation Kwargs

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, mock, workflow, integration

## Overview

Workflow: test compilation kwargs

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `unittest.mock`
- `numpy`
- `pytest`
- `scipy.stats`
- `arviz_base`
- `pytensor.compile`
- `pymc.distributions`
- `pymc.distributions.transforms`
- `pymc.model`
- `pymc.stats.log_density`
- `tests.distributions.test_multivariate`

**Setup Required:**
```python
# Fixtures: via
```

## Step-by-Step Guide

### Step 1: Assign x = Normal(...)

```python
x = Normal('x')
```

**Verification:**
```python
assert len(patched_compile.call_args_list) == 2
```

### Step 2: Call Deterministic()

```python
Deterministic('d', 2 * x)
```

**Verification:**
```python
assert get_mode(patched_compile.call_args_list[0].kwargs['mode']) == get_mode('JAX')
```

### Step 3: Call Normal()

```python
Normal('y', x, observed=[0, 1, 2])
```

**Verification:**
```python
assert get_mode(patched_compile.call_args_list[1].kwargs['mode']) == get_mode('NUMBA')
```

### Step 4: Assign idata = from_dict(...)

```python
idata = from_dict({'posterior': {'x': np.arange(100).reshape(4, 25)}})
```

### Step 5: Assign prior_kwargs = value

```python
prior_kwargs = {'compile_kwargs': {'mode': 'JAX'}} if via == 'compile_kwargs' else {'backend': 'JAX'}
```

### Step 6: Assign lik_kwargs = value

```python
lik_kwargs = {'compile_kwargs': {'mode': 'NUMBA'}} if via == 'compile_kwargs' else {'backend': 'NUMBA'}
```

### Step 7: Call compute_log_prior()

```python
compute_log_prior(idata, extend_inferencedata=False, **prior_kwargs)
```

### Step 8: Call compute_log_likelihood()

```python
compute_log_likelihood(idata, extend_inferencedata=False, **lik_kwargs)
```


## Complete Example

```python
# Setup
# Fixtures: via

# Workflow
with Model() as m:
    x = Normal('x')
    Deterministic('d', 2 * x)
    Normal('y', x, observed=[0, 1, 2])
    idata = from_dict({'posterior': {'x': np.arange(100).reshape(4, 25)}})
    prior_kwargs = {'compile_kwargs': {'mode': 'JAX'}} if via == 'compile_kwargs' else {'backend': 'JAX'}
    lik_kwargs = {'compile_kwargs': {'mode': 'NUMBA'}} if via == 'compile_kwargs' else {'backend': 'NUMBA'}
    with patch('pymc.stats.log_density.apply_function_over_dataset'), patch('pymc.model.core.compile') as patched_compile:
        compute_log_prior(idata, extend_inferencedata=False, **prior_kwargs)
        compute_log_likelihood(idata, extend_inferencedata=False, **lik_kwargs)
assert len(patched_compile.call_args_list) == 2
assert get_mode(patched_compile.call_args_list[0].kwargs['mode']) == get_mode('JAX')
assert get_mode(patched_compile.call_args_list[1].kwargs['mode']) == get_mode('NUMBA')
```

## Next Steps


---

*Source: test_log_density.py:182 | Complexity: Advanced | Last updated: 2026-05-18*