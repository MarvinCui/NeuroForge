# How To: Unvalued Rv Model

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test unvalued rv model

## Prerequisites

**Required Modules:**
- `numpy`
- `pytensor`
- `pytest`
- `pytensor`
- `pytensor`
- `pytensor.compile`
- `pytensor.graph.basic`
- `pytensor.graph.replace`
- `pytensor.graph.traversal`
- `pytensor.tensor.random.basic`
- `pytensor.tensor.random.op`
- `pymc`
- `pymc.distributions.distribution`
- `pymc.distributions.transforms`
- `pymc.logprob.abstract`
- `pymc.logprob.basic`
- `pymc.logprob.utils`
- `pymc.testing`
- `tests.logprob.utils`


## Step-by-Step Guide

### Step 1: Assign x_value = value

```python
x_value = m.rvs_to_values[x]
```

**Verification:**
```python
assert res.owner.op == pt.add
```

### Step 2: Assign z_value = value

```python
z_value = m.rvs_to_values[z]
```

**Verification:**
```python
assert res.owner.inputs[0] is z_value
```

### Step 3: Assign unknown = replace_rvs_by_values(...)

```python
res, = replace_rvs_by_values((out,), rvs_to_values=m.rvs_to_values, rvs_to_transforms=m.rvs_to_transforms)
```

**Verification:**
```python
assert res_y is not y
```

### Step 4: Assign res_y = value

```python
res_y = res.owner.inputs[1]
```

**Verification:**
```python
assert isinstance(res_y.owner.op, NormalRV)
```

### Step 5: Assign x = pm.Normal(...)

```python
x = pm.Normal('x')
```

**Verification:**
```python
assert res_y.owner.inputs[2] is x_value
```

### Step 6: Assign y = pm.Normal.dist(...)

```python
y = pm.Normal.dist(x)
```

### Step 7: Assign z = pm.Normal(...)

```python
z = pm.Normal('z', y)
```

### Step 8: Assign out = value

```python
out = z + y
```


## Complete Example

```python
# Workflow
with pm.Model() as m:
    x = pm.Normal('x')
    y = pm.Normal.dist(x)
    z = pm.Normal('z', y)
    out = z + y
x_value = m.rvs_to_values[x]
z_value = m.rvs_to_values[z]
res, = replace_rvs_by_values((out,), rvs_to_values=m.rvs_to_values, rvs_to_transforms=m.rvs_to_transforms)
assert res.owner.op == pt.add
assert res.owner.inputs[0] is z_value
res_y = res.owner.inputs[1]
assert res_y is not y
assert isinstance(res_y.owner.op, NormalRV)
assert res_y.owner.inputs[2] is x_value
```

## Next Steps


---

*Source: test_utils.py:162 | Complexity: Advanced | Last updated: 2026-05-18*