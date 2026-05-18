# How To: Uniform

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test uniform

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

### Step 2: Assign model = self.build_model(...)

```python
model = self.build_model(pm.Uniform, {'lower': lower, 'upper': upper}, size=size, transform=interval)
```

### Step 3: Call self.check_transform_elementwise_logp()

```python
self.check_transform_elementwise_logp(model)
```

### Step 4: Assign unknown = inputs

```python
_, _, lower, upper = inputs
```

### Step 5: Assign lower = value

```python
lower = pt.as_tensor_variable(lower) if lower is not None else None
```

### Step 6: Assign upper = value

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
model = self.build_model(pm.Uniform, {'lower': lower, 'upper': upper}, size=size, transform=interval)
self.check_transform_elementwise_logp(model)
```

## Next Steps


---

*Source: test_transform.py:415 | Complexity: Intermediate | Last updated: 2026-05-18*