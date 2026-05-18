# How To: Vectorize Over Posterior With Intermediate Rvs

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test vectorize over posterior with intermediate rvs

## Prerequisites

**Required Modules:**
- `logging`
- `warnings`
- `contextlib`
- `numpy`
- `numpy.random`
- `numpy.testing`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `xarray`
- `arviz_base`
- `arviz_base.testing`
- `pytensor`
- `pytensor.compile`
- `pytensor.graph`
- `pytensor.graph.traversal`
- `pytensor.tensor.variable`
- `scipy`
- `pymc`
- `pymc.backends.base`
- `pymc.distributions.shape_utils`
- `pymc.exceptions`
- `pymc.model.transform.conditioning`
- `pymc.model.transform.optimization`
- `pymc.pytensorf`
- `pymc.sampling.forward`
- `pymc.testing`


## Step-by-Step Guide

### Step 1: Assign unknown = vectorize_over_posterior(...)

```python
_, _, vectorized_no_intermediate = vectorize_over_posterior(outputs=[b, c, d], posterior=idata.posterior, input_rvs=[a], allow_rvs_in_graph=True)
```

**Verification:**
```python
assert vectorized_no_intermediate.type.shape == (1, 100)
```

### Step 2: Assign unknown = vectorize_over_posterior(...)

```python
[vectorized_intermediate_rvs] = vectorize_over_posterior(outputs=[d], posterior=idata.posterior, input_rvs=[a], allow_rvs_in_graph=True)
```

**Verification:**
```python
assert vectorized_no_intermediate.type.shape == vectorized_intermediate_rvs.type.shape
```

### Step 3: Assign unknown = get_var_by_name(...)

```python
[a_ancestor1] = get_var_by_name([vectorized_no_intermediate], 'a')
```

**Verification:**
```python
assert isinstance(a_ancestor1, TensorConstant)
```

### Step 4: Assign unknown = get_var_by_name(...)

```python
[a_ancestor2] = get_var_by_name([vectorized_intermediate_rvs], 'a')
```

**Verification:**
```python
assert np.array_equiv(a_ancestor1.eval(), idata.posterior.a.data)
```

### Step 5: Assign a = pm.Normal(...)

```python
a = pm.Normal('a')
```

**Verification:**
```python
assert isinstance(a_ancestor2, TensorConstant)
```

### Step 6: Assign b = pm.Normal.dist(...)

```python
b = pm.Normal.dist(a)
```

**Verification:**
```python
assert np.array_equiv(a_ancestor2.eval(), idata.posterior.a.data)
```

### Step 7: Assign c = value

```python
c = b + 1
```

### Step 8: Assign d = pm.Normal.dist(...)

```python
d = pm.Normal.dist(c)
```

### Step 9: Assign idata = pm.sample_prior_predictive(...)

```python
idata = pm.sample_prior_predictive(100, var_names=['a'])
```

### Step 10: Call idata.update()

```python
idata.update({'posterior': idata.prior})
```


## Complete Example

```python
# Workflow
with pm.Model() as model:
    a = pm.Normal('a')
    b = pm.Normal.dist(a)
    c = b + 1
    d = pm.Normal.dist(c)
    idata = pm.sample_prior_predictive(100, var_names=['a'])
    idata.update({'posterior': idata.prior})
_, _, vectorized_no_intermediate = vectorize_over_posterior(outputs=[b, c, d], posterior=idata.posterior, input_rvs=[a], allow_rvs_in_graph=True)
[vectorized_intermediate_rvs] = vectorize_over_posterior(outputs=[d], posterior=idata.posterior, input_rvs=[a], allow_rvs_in_graph=True)
assert vectorized_no_intermediate.type.shape == (1, 100)
assert vectorized_no_intermediate.type.shape == vectorized_intermediate_rvs.type.shape
[a_ancestor1] = get_var_by_name([vectorized_no_intermediate], 'a')
[a_ancestor2] = get_var_by_name([vectorized_intermediate_rvs], 'a')
assert isinstance(a_ancestor1, TensorConstant)
assert np.array_equiv(a_ancestor1.eval(), idata.posterior.a.data)
assert isinstance(a_ancestor2, TensorConstant)
assert np.array_equiv(a_ancestor2.eval(), idata.posterior.a.data)
```

## Next Steps


---

*Source: test_forward.py:2276 | Complexity: Advanced | Last updated: 2026-05-18*