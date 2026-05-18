# How To: Measurable Power Exponent With Variable Base

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test measurable power exponent with variable base

## Prerequisites

**Required Modules:**
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `scipy`
- `scipy.special`
- `pytensor.graph.basic`
- `pymc.distributions.continuous`
- `pymc.distributions.discrete`
- `pymc.logprob.basic`
- `pymc.logprob.transforms`
- `pymc.logprob.utils`
- `pymc.testing`
- `tests.distributions.test_transform`


## Step-by-Step Guide

### Step 1: Assign base_rv = pt.random.normal(...)

```python
base_rv = pt.random.normal([2])
```

### Step 2: Assign x_raw_rv = pt.random.normal(...)

```python
x_raw_rv = pt.random.normal()
```

### Step 3: Assign x_rv = pt.power(...)

```python
x_rv = pt.power(base_rv, x_raw_rv)
```

### Step 4: Assign x_rv.name = 'x'

```python
x_rv.name = 'x'
```

### Step 5: Assign base_rv.name = 'base'

```python
base_rv.name = 'base'
```

### Step 6: Assign base_vv = base_rv.clone(...)

```python
base_vv = base_rv.clone()
```

### Step 7: Assign x_vv = x_rv.clone(...)

```python
x_vv = x_rv.clone()
```

### Step 8: Assign res = conditional_logp(...)

```python
res = conditional_logp({base_rv: base_vv, x_rv: x_vv})
```

### Step 9: Assign x_logp = value

```python
x_logp = res[x_vv]
```

### Step 10: Assign logp_vals_fn = pytensor.function(...)

```python
logp_vals_fn = pytensor.function([base_vv, x_vv], x_logp)
```

### Step 11: Call logp_vals_fn()

```python
logp_vals_fn(np.array([-2]), np.array([2]))
```


## Complete Example

```python
# Workflow
base_rv = pt.random.normal([2])
x_raw_rv = pt.random.normal()
x_rv = pt.power(base_rv, x_raw_rv)
x_rv.name = 'x'
base_rv.name = 'base'
base_vv = base_rv.clone()
x_vv = x_rv.clone()
res = conditional_logp({base_rv: base_vv, x_rv: x_vv})
x_logp = res[x_vv]
logp_vals_fn = pytensor.function([base_vv, x_vv], x_logp)
with pytest.raises(ParameterValueError, match='base >= 0'):
    logp_vals_fn(np.array([-2]), np.array([2]))
```

## Next Steps


---

*Source: test_transforms.py:654 | Complexity: Advanced | Last updated: 2026-05-18*