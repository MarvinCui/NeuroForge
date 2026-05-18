# How To: Distinct Rvs

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Make sure `RandomVariable`s generated using a `Model`'s default RNG state all have distinct states.

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

### Step 1: "Make sure `RandomVariable`s generated using a `Model`'s default RNG state all have distinct states."

```python
"Make sure `RandomVariable`s generated using a `Model`'s default RNG state all have distinct states."
```

**Verification:**
```python
assert X_rv.owner.inputs[0] != Y_rv.owner.inputs[0]
```

### Step 2: Assign X_rv = pm.Normal(...)

```python
X_rv = pm.Normal('x')
```

**Verification:**
```python
assert np.array_equal(pp_samples['y'], pp_samples_2['y'])
```

### Step 3: Assign Y_rv = pm.Normal(...)

```python
Y_rv = pm.Normal('y')
```

### Step 4: Assign pp_samples = pm.sample_prior_predictive(...)

```python
pp_samples = pm.sample_prior_predictive(draws=2, return_inferencedata=False, random_seed=npr.default_rng(2023532))
```

### Step 5: Assign X_rv = pm.Normal(...)

```python
X_rv = pm.Normal('x')
```

### Step 6: Assign Y_rv = pm.Normal(...)

```python
Y_rv = pm.Normal('y')
```

### Step 7: Assign pp_samples_2 = pm.sample_prior_predictive(...)

```python
pp_samples_2 = pm.sample_prior_predictive(draws=2, return_inferencedata=False, random_seed=npr.default_rng(2023532))
```


## Complete Example

```python
# Workflow
"Make sure `RandomVariable`s generated using a `Model`'s default RNG state all have distinct states."
with pm.Model() as model:
    X_rv = pm.Normal('x')
    Y_rv = pm.Normal('y')
    pp_samples = pm.sample_prior_predictive(draws=2, return_inferencedata=False, random_seed=npr.default_rng(2023532))
assert X_rv.owner.inputs[0] != Y_rv.owner.inputs[0]
with pm.Model():
    X_rv = pm.Normal('x')
    Y_rv = pm.Normal('y')
    pp_samples_2 = pm.sample_prior_predictive(draws=2, return_inferencedata=False, random_seed=npr.default_rng(2023532))
assert np.array_equal(pp_samples['y'], pp_samples_2['y'])
```

## Next Steps


---

*Source: test_forward.py:1748 | Complexity: Intermediate | Last updated: 2026-05-18*