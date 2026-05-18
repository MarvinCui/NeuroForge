# How To: Uniform Ordered

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test uniform ordered

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytensor.tensor`
- `pytest`
- `numpy.testing`
- `pytensor`
- `pytensor.tensor.variable`
- `pymc`
- `pymc.distributions.transforms`
- `pymc.logprob.basic`
- `pymc.logprob.transforms`
- `pymc.pytensorf`
- `pymc.testing`
- `numpy`

**Setup Required:**
```python
# Fixtures: lower, upper, size
```

## Step-by-Step Guide

### Step 1: Assign interval = tr.Interval(...)

```python
interval = tr.Interval(bounds_fn=transform_params)
```

### Step 2: Assign initval = np.sort(...)

```python
initval = np.sort(np.abs(np.random.rand(*size)))
```

### Step 3: Assign model = self.build_model(...)

```python
model = self.build_model(pm.Uniform, {'lower': lower, 'upper': upper}, size=size, initval=initval, transform=tr.Chain([interval, tr.ordered]))
```

### Step 4: Call self.check_vectortransform_elementwise_logp()

```python
self.check_vectortransform_elementwise_logp(model)
```

### Step 5: Assign unknown = inputs

```python
_, _, lower, upper = inputs
```

### Step 6: Assign lower = value

```python
lower = pt.as_tensor_variable(lower) if lower is not None else None
```

### Step 7: Assign upper = value

```python
upper = pt.as_tensor_variable(upper) if upper is not None else None
```


## Complete Example

```python
# Setup
# Fixtures: lower, upper, size

# Workflow
def transform_params(*inputs):
    _, _, lower, upper = inputs
    lower = pt.as_tensor_variable(lower) if lower is not None else None
    upper = pt.as_tensor_variable(upper) if upper is not None else None
    return (lower, upper)
interval = tr.Interval(bounds_fn=transform_params)
initval = np.sort(np.abs(np.random.rand(*size)))
model = self.build_model(pm.Uniform, {'lower': lower, 'upper': upper}, size=size, initval=initval, transform=tr.Chain([interval, tr.ordered]))
self.check_vectortransform_elementwise_logp(model)
```

## Next Steps


---

*Source: test_transform.py:532 | Complexity: Intermediate | Last updated: 2026-05-18*