# How To: Make Obs Var

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Check returned values for `data` given known inputs to `as_tensor()`.

Note that ndarrays should return a TensorConstant and sparse inputs
should return a Sparse PyTensor object.

## Prerequisites

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


## Step-by-Step Guide

### Step 1: '\n    Check returned values for `data` given known inputs to `as_tensor()`.\n\n    Note that ndarrays should return a TensorConstant and sparse inputs\n    should return a Sparse PyTensor object.\n    '

```python
'\n    Check returned values for `data` given known inputs to `as_tensor()`.\n\n    Note that ndarrays should return a TensorConstant and sparse inputs\n    should return a Sparse PyTensor object.\n    '
```

**Verification:**
```python
assert dense_output == fake_distribution
```

### Step 2: Assign input_name = 'testing_inputs'

```python
input_name = 'testing_inputs'
```

**Verification:**
```python
assert isinstance(fake_model.rvs_to_values[dense_output], TensorConstant)
```

### Step 3: Assign sparse_input = sps.csr_matrix(...)

```python
sparse_input = sps.csr_matrix(np.eye(3))
```

**Verification:**
```python
assert sparse_output == fake_distribution
```

### Step 4: Assign dense_input = np.arange.reshape(...)

```python
dense_input = np.arange(9).reshape((3, 3))
```

**Verification:**
```python
assert sparse.basic._is_sparse_variable(fake_model.rvs_to_values[sparse_output])
```

### Step 5: Assign masked_array_input = ma.array(...)

```python
masked_array_input = ma.array(dense_input, mask=np.mod(dense_input, 2) == 0)
```

**Verification:**
```python
assert masked_output != fake_distribution
```

### Step 6: Assign fake_model = pm.Model(...)

```python
fake_model = pm.Model()
```

**Verification:**
```python
assert not isinstance(masked_output, RandomVariable)
```

### Step 7: Assign dense_output = fake_model.make_obs_var(...)

```python
dense_output = fake_model.make_obs_var(fake_distribution, dense_input, None, None, None, None)
```

**Verification:**
```python
assert {'testing_inputs_unobserved'} == {v.name for v in fake_model.value_vars}
```

### Step 8: Assign sparse_output = fake_model.make_obs_var(...)

```python
sparse_output = fake_model.make_obs_var(fake_distribution, sparse_input, None, None, None, None)
```

**Verification:**
```python
assert {'testing_inputs', 'testing_inputs_observed'} == {v.name for v in fake_model.observed_RVs}
```

### Step 9: Assign scaled_outputs = fake_model.make_obs_var(...)

```python
scaled_outputs = fake_model.make_obs_var(fake_distribution, dense_input, None, None, None, total_size=100)
```

**Verification:**
```python
assert scaled_outputs != fake_distribution
```

### Step 10: Assign fake_distribution = pm.Normal.dist(...)

```python
fake_distribution = pm.Normal.dist(mu=0, sigma=1, size=(3, 3))
```

**Verification:**
```python
assert isinstance(scaled_outputs.owner.op, MinibatchRandomVariable)
```

### Step 11: Assign fake_distribution.name = input_name

```python
fake_distribution.name = input_name
```

### Step 12: Call fake_model.make_obs_var()

```python
fake_model.make_obs_var(fake_distribution, np.ones((3, 3, 1)), None, None, None, None)
```

### Step 13: Assign masked_output = fake_model.make_obs_var(...)

```python
masked_output = fake_model.make_obs_var(fake_distribution, masked_array_input, None, None, None, None)
```


## Complete Example

```python
# Workflow
'\n    Check returned values for `data` given known inputs to `as_tensor()`.\n\n    Note that ndarrays should return a TensorConstant and sparse inputs\n    should return a Sparse PyTensor object.\n    '
input_name = 'testing_inputs'
sparse_input = sps.csr_matrix(np.eye(3))
dense_input = np.arange(9).reshape((3, 3))
masked_array_input = ma.array(dense_input, mask=np.mod(dense_input, 2) == 0)
fake_model = pm.Model()
with fake_model:
    fake_distribution = pm.Normal.dist(mu=0, sigma=1, size=(3, 3))
    fake_distribution.name = input_name
with pytest.raises(ShapeError, match="Dimensionality of data and RV don't match."):
    fake_model.make_obs_var(fake_distribution, np.ones((3, 3, 1)), None, None, None, None)
dense_output = fake_model.make_obs_var(fake_distribution, dense_input, None, None, None, None)
assert dense_output == fake_distribution
assert isinstance(fake_model.rvs_to_values[dense_output], TensorConstant)
del fake_model.named_vars[fake_distribution.name]
sparse_output = fake_model.make_obs_var(fake_distribution, sparse_input, None, None, None, None)
assert sparse_output == fake_distribution
assert sparse.basic._is_sparse_variable(fake_model.rvs_to_values[sparse_output])
del fake_model.named_vars[fake_distribution.name]
with pytest.warns(ImputationWarning):
    masked_output = fake_model.make_obs_var(fake_distribution, masked_array_input, None, None, None, None)
assert masked_output != fake_distribution
assert not isinstance(masked_output, RandomVariable)
assert {'testing_inputs_unobserved'} == {v.name for v in fake_model.value_vars}
assert {'testing_inputs', 'testing_inputs_observed'} == {v.name for v in fake_model.observed_RVs}
del fake_model.named_vars[fake_distribution.name]
scaled_outputs = fake_model.make_obs_var(fake_distribution, dense_input, None, None, None, total_size=100)
assert scaled_outputs != fake_distribution
assert isinstance(scaled_outputs.owner.op, MinibatchRandomVariable)
del fake_model.named_vars[fake_distribution.name]
```

## Next Steps


---

*Source: test_core.py:629 | Complexity: Advanced | Last updated: 2026-05-18*