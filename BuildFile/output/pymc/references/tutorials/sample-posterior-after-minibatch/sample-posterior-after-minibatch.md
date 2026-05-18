# How To: Sample Posterior After Minibatch

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test sample posterior after minibatch

## Prerequisites

**Required Modules:**
- `io`
- `operator`
- `warnings`
- `cloudpickle`
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `pymc`
- `pymc.variational.opvi`
- `pymc.model.transform.basic`
- `pymc.pytensorf`
- `pymc.variational.inference`
- `pymc.variational.opvi`
- `tests`


## Step-by-Step Guide

### Step 1: Assign model_post = remove_minibatched_nodes(...)

```python
model_post = remove_minibatched_nodes(model)
```

**Verification:**
```python
assert trace.posterior['beta'].shape == (1, 500)
```

### Step 2: Assign x = pm.Data(...)

```python
x = pm.Data('x', [1.0, 2.0, 3.0], dims='obs_id')
```

**Verification:**
```python
assert trace.constant_data['x'].shape == (3,)
```

### Step 3: Assign y = pm.Data(...)

```python
y = pm.Data('y', [1.0, 2.0, 3.0], dims='obs_id')
```

**Verification:**
```python
assert trace.observed_data['obs'].shape == (3,)
```

### Step 4: Assign unknown = pm.Minibatch(...)

```python
x_mini, y_mini = pm.Minibatch(x, y, batch_size=2)
```

**Verification:**
```python
assert y_test.predictions['obs'].shape == (1, 500, 5)
```

### Step 5: Assign beta = pm.Normal(...)

```python
beta = pm.Normal('beta', 0, 10.0)
```

### Step 6: Assign y_hat = pm.Deterministic(...)

```python
y_hat = pm.Deterministic('y_hat', beta * x_mini, dims='obs_id')
```

### Step 7: Call pm.Normal()

```python
pm.Normal('obs', y_hat, np.sqrt(0.01), observed=y_mini, total_size=3, dims='obs_id')
```

### Step 8: Assign approx = pm.fit(...)

```python
approx = pm.fit(10, method='advi', progressbar=False)
```

### Step 9: Assign trace = approx.sample(...)

```python
trace = approx.sample(500)
```

### Step 10: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', 'Numba will use object mode', UserWarning)
```

### Step 11: Assign x_test = value

```python
x_test = [5, 6, 9, 12, 15]
```

### Step 12: Call pm.set_data()

```python
pm.set_data(new_data={'x': x_test, 'y': [0.0] * len(x_test)}, coords={'obs_id': list(range(len(x_test)))})
```

### Step 13: Assign y_test = pm.sample_posterior_predictive(...)

```python
y_test = pm.sample_posterior_predictive(trace, predictions=True, progressbar=False)
```


## Complete Example

```python
# Workflow
with pm.Model(coords={'obs_id': [0, 1, 2]}) as model:
    x = pm.Data('x', [1.0, 2.0, 3.0], dims='obs_id')
    y = pm.Data('y', [1.0, 2.0, 3.0], dims='obs_id')
    x_mini, y_mini = pm.Minibatch(x, y, batch_size=2)
    beta = pm.Normal('beta', 0, 10.0)
    y_hat = pm.Deterministic('y_hat', beta * x_mini, dims='obs_id')
    pm.Normal('obs', y_hat, np.sqrt(0.01), observed=y_mini, total_size=3, dims='obs_id')
    approx = pm.fit(10, method='advi', progressbar=False)
model_post = remove_minibatched_nodes(model)
with model_post:
    trace = approx.sample(500)
assert trace.posterior['beta'].shape == (1, 500)
assert trace.constant_data['x'].shape == (3,)
assert trace.observed_data['obs'].shape == (3,)
with model_post, warnings.catch_warnings():
    warnings.filterwarnings('ignore', 'Numba will use object mode', UserWarning)
    x_test = [5, 6, 9, 12, 15]
    pm.set_data(new_data={'x': x_test, 'y': [0.0] * len(x_test)}, coords={'obs_id': list(range(len(x_test)))})
    y_test = pm.sample_posterior_predictive(trace, predictions=True, progressbar=False)
assert y_test.predictions['obs'].shape == (1, 500, 5)
```

## Next Steps


---

*Source: test_inference.py:452 | Complexity: Advanced | Last updated: 2026-05-18*