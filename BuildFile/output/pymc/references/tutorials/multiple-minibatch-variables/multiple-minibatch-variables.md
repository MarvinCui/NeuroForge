# How To: Multiple Minibatch Variables

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Regression test for bug reported in
https://discourse.pymc.io/t/verifying-that-minibatch-is-actually-randomly-sampling/14308

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

### Step 1: 'Regression test for bug reported in\n    https://discourse.pymc.io/t/verifying-that-minibatch-is-actually-randomly-sampling/14308\n    '

```python
'Regression test for bug reported in\n    https://discourse.pymc.io/t/verifying-that-minibatch-is-actually-randomly-sampling/14308\n    '
```

### Step 2: Assign true_weights = np.array(...)

```python
true_weights = np.array([-5, 5] * 5)
```

### Step 3: Assign feature = np.repeat(...)

```python
feature = np.repeat(np.eye(10), 10000, axis=0)
```

### Step 4: Assign y = value

```python
y = feature @ true_weights
```

### Step 5: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(mean_field.mean.get_value(), true_weights, rtol=0.1)
```

### Step 6: Assign unknown = pm.Minibatch(...)

```python
minibatch_feature, minibatch_y = pm.Minibatch(feature, y, batch_size=1)
```

### Step 7: Assign weights = pm.Normal(...)

```python
weights = pm.Normal('weights', 0, 10, shape=10)
```

### Step 8: Call pm.Normal()

```python
pm.Normal('y', mu=minibatch_feature @ weights, sigma=0.01, observed=minibatch_y, total_size=len(y))
```

### Step 9: Assign mean_field = pm.fit(...)

```python
mean_field = pm.fit(10000, obj_optimizer=pm.adam(learning_rate=0.01), progressbar=False)
```


## Complete Example

```python
# Workflow
'Regression test for bug reported in\n    https://discourse.pymc.io/t/verifying-that-minibatch-is-actually-randomly-sampling/14308\n    '
true_weights = np.array([-5, 5] * 5)
feature = np.repeat(np.eye(10), 10000, axis=0)
y = feature @ true_weights
with pm.Model() as model:
    minibatch_feature, minibatch_y = pm.Minibatch(feature, y, batch_size=1)
    weights = pm.Normal('weights', 0, 10, shape=10)
    pm.Normal('y', mu=minibatch_feature @ weights, sigma=0.01, observed=minibatch_y, total_size=len(y))
    mean_field = pm.fit(10000, obj_optimizer=pm.adam(learning_rate=0.01), progressbar=False)
np.testing.assert_allclose(mean_field.mean.get_value(), true_weights, rtol=0.1)
```

## Next Steps


---

*Source: test_inference.py:486 | Complexity: Advanced | Last updated: 2026-05-18*