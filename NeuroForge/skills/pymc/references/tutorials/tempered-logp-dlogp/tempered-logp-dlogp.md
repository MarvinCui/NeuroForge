# How To: Tempered Logp Dlogp

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test tempered logp dlogp

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `copy`
- `pickle`
- `threading`
- `traceback`
- `warnings`
- `unittest.mock`
- `arviz`
- `cloudpickle`
- `numpy`
- `numpy.ma`
- `numpy.testing`
- `pytensor`
- `pytensor.sparse`
- `pytensor.tensor`
- `pytest`
- `scipy`
- `scipy.sparse`
- `scipy.stats`
- `pytensor.compile.mode`
- `pytensor.graph`
- `pytensor.graph.traversal`
- `pytensor.link.numba`
- `pytensor.raise_op`
- `pytensor.tensor.random.op`
- `pytensor.tensor.variable`
- `pymc`
- `pymc`
- `pymc.blocking`
- `pymc.distributions`
- `pymc.distributions.distribution`
- `pymc.distributions.transforms`
- `pymc.exceptions`
- `pymc.logprob.basic`
- `pymc.logprob.transforms`
- `pymc.model`
- `pymc.pytensorf`
- `pymc.variational.minibatch_rv`
- `tests.models`

**Setup Required:**
```python
# Fixtures: ravel_inputs
```

## Step-by-Step Guide

### Step 1: Assign func = model.logp_dlogp_function(...)

```python
func = model.logp_dlogp_function(ravel_inputs=ravel_inputs)
```

### Step 2: Call func.set_extra_values()

```python
func.set_extra_values({})
```

### Step 3: Assign func_temp = model.logp_dlogp_function(...)

```python
func_temp = model.logp_dlogp_function(tempered=True, ravel_inputs=ravel_inputs)
```

### Step 4: Call func_temp.set_extra_values()

```python
func_temp.set_extra_values({})
```

### Step 5: Assign func_nograd = model.logp_dlogp_function(...)

```python
func_nograd = model.logp_dlogp_function(compute_grads=False, ravel_inputs=ravel_inputs)
```

### Step 6: Call func_nograd.set_extra_values()

```python
func_nograd.set_extra_values({})
```

### Step 7: Assign func_temp_nograd = model.logp_dlogp_function(...)

```python
func_temp_nograd = model.logp_dlogp_function(tempered=True, compute_grads=False, ravel_inputs=ravel_inputs)
```

### Step 8: Call func_temp_nograd.set_extra_values()

```python
func_temp_nograd.set_extra_values({})
```

### Step 9: Assign x = np.ones(...)

```python
x = np.ones((1,), dtype=func.dtype)
```

### Step 10: Call npt.assert_allclose()

```python
npt.assert_allclose(func(x)[0], func_temp(x)[0])
```

### Step 11: Call npt.assert_allclose()

```python
npt.assert_allclose(func(x)[1], func_temp(x)[1])
```

### Step 12: Call npt.assert_allclose()

```python
npt.assert_allclose(func_nograd(x), func(x)[0])
```

### Step 13: Call npt.assert_allclose()

```python
npt.assert_allclose(func_temp_nograd(x), func(x)[0])
```

### Step 14: Call func_temp.set_weights()

```python
func_temp.set_weights(np.array([0.0], dtype=func.dtype))
```

### Step 15: Call func_temp_nograd.set_weights()

```python
func_temp_nograd.set_weights(np.array([0.0], dtype=func.dtype))
```

### Step 16: Call npt.assert_allclose()

```python
npt.assert_allclose(func(x)[0], 2 * func_temp(x)[0] - 1)
```

### Step 17: Call npt.assert_allclose()

```python
npt.assert_allclose(func(x)[1], func_temp(x)[1])
```

### Step 18: Call npt.assert_allclose()

```python
npt.assert_allclose(func_nograd(x), func(x)[0])
```

### Step 19: Call npt.assert_allclose()

```python
npt.assert_allclose(func_temp_nograd(x), func_temp(x)[0])
```

### Step 20: Call func_temp.set_weights()

```python
func_temp.set_weights(np.array([0.5], dtype=func.dtype))
```

### Step 21: Call func_temp_nograd.set_weights()

```python
func_temp_nograd.set_weights(np.array([0.5], dtype=func.dtype))
```

### Step 22: Call npt.assert_allclose()

```python
npt.assert_allclose(func(x)[0], 4 / 3 * (func_temp(x)[0] - 1 / 4))
```

### Step 23: Call npt.assert_allclose()

```python
npt.assert_allclose(func(x)[1], func_temp(x)[1])
```

### Step 24: Call npt.assert_allclose()

```python
npt.assert_allclose(func_nograd(x), func(x)[0])
```

### Step 25: Call npt.assert_allclose()

```python
npt.assert_allclose(func_temp_nograd(x), func_temp(x)[0])
```

### Step 26: Call pm.Normal()

```python
pm.Normal('x')
```

### Step 27: Call pm.Normal()

```python
pm.Normal('y', observed=1)
```

### Step 28: Call pm.Potential()

```python
pm.Potential('z', pt.constant(-1.0, dtype=pytensor.config.floatX))
```


## Complete Example

```python
# Setup
# Fixtures: ravel_inputs

# Workflow
with pm.Model() as model:
    pm.Normal('x')
    pm.Normal('y', observed=1)
    pm.Potential('z', pt.constant(-1.0, dtype=pytensor.config.floatX))
func = model.logp_dlogp_function(ravel_inputs=ravel_inputs)
func.set_extra_values({})
func_temp = model.logp_dlogp_function(tempered=True, ravel_inputs=ravel_inputs)
func_temp.set_extra_values({})
func_nograd = model.logp_dlogp_function(compute_grads=False, ravel_inputs=ravel_inputs)
func_nograd.set_extra_values({})
func_temp_nograd = model.logp_dlogp_function(tempered=True, compute_grads=False, ravel_inputs=ravel_inputs)
func_temp_nograd.set_extra_values({})
x = np.ones((1,), dtype=func.dtype)
npt.assert_allclose(func(x)[0], func_temp(x)[0])
npt.assert_allclose(func(x)[1], func_temp(x)[1])
npt.assert_allclose(func_nograd(x), func(x)[0])
npt.assert_allclose(func_temp_nograd(x), func(x)[0])
func_temp.set_weights(np.array([0.0], dtype=func.dtype))
func_temp_nograd.set_weights(np.array([0.0], dtype=func.dtype))
npt.assert_allclose(func(x)[0], 2 * func_temp(x)[0] - 1)
npt.assert_allclose(func(x)[1], func_temp(x)[1])
npt.assert_allclose(func_nograd(x), func(x)[0])
npt.assert_allclose(func_temp_nograd(x), func_temp(x)[0])
func_temp.set_weights(np.array([0.5], dtype=func.dtype))
func_temp_nograd.set_weights(np.array([0.5], dtype=func.dtype))
npt.assert_allclose(func(x)[0], 4 / 3 * (func_temp(x)[0] - 1 / 4))
npt.assert_allclose(func(x)[1], func_temp(x)[1])
npt.assert_allclose(func_nograd(x), func(x)[0])
npt.assert_allclose(func_temp_nograd(x), func_temp(x)[0])
```

## Next Steps


---

*Source: test_core.py:494 | Complexity: Advanced | Last updated: 2026-05-18*