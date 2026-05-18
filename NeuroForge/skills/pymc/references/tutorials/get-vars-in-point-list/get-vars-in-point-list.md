# How To: Get Vars In Point List

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test get vars in point list

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

### Step 1: Assign point_list = value

```python
point_list = [{'a': 0, 'b': 0, 'd': 0}]
```

**Verification:**
```python
assert set(vars_in_trace) == {a}
```

### Step 2: Assign vars_in_trace = get_vars_in_point_list(...)

```python
vars_in_trace = get_vars_in_point_list(point_list, modelB)
```

**Verification:**
```python
assert set(vars_in_trace) == {a}
```

### Step 3: Assign strace = pm.backends.NDArray(...)

```python
strace = pm.backends.NDArray(model=modelB, vars=modelA.free_RVs)
```

### Step 4: Call strace.setup()

```python
strace.setup(1, 1)
```

### Step 5: Assign strace.values = value

```python
strace.values = point_list[0]
```

### Step 6: Assign strace.draw_idx = 1

```python
strace.draw_idx = 1
```

### Step 7: Assign trace = MultiTrace(...)

```python
trace = MultiTrace([strace])
```

### Step 8: Assign vars_in_trace = get_vars_in_point_list(...)

```python
vars_in_trace = get_vars_in_point_list(trace, modelB)
```

**Verification:**
```python
assert set(vars_in_trace) == {a}
```

### Step 9: Call pm.Normal()

```python
pm.Normal('a', 0, 1)
```

### Step 10: Call pm.Normal()

```python
pm.Normal('b', 0, 1)
```

### Step 11: Call pm.Normal()

```python
pm.Normal('d', 0, 1)
```

### Step 12: Assign a = pm.Normal(...)

```python
a = pm.Normal('a', 0, 1)
```

### Step 13: Call pm.Normal()

```python
pm.Normal('c', 0, 1)
```

### Step 14: Call pm.Data()

```python
pm.Data('d', 0)
```


## Complete Example

```python
# Workflow
with pm.Model() as modelA:
    pm.Normal('a', 0, 1)
    pm.Normal('b', 0, 1)
    pm.Normal('d', 0, 1)
with pm.Model() as modelB:
    a = pm.Normal('a', 0, 1)
    pm.Normal('c', 0, 1)
    pm.Data('d', 0)
point_list = [{'a': 0, 'b': 0, 'd': 0}]
vars_in_trace = get_vars_in_point_list(point_list, modelB)
assert set(vars_in_trace) == {a}
strace = pm.backends.NDArray(model=modelB, vars=modelA.free_RVs)
strace.setup(1, 1)
strace.values = point_list[0]
strace.draw_idx = 1
trace = MultiTrace([strace])
vars_in_trace = get_vars_in_point_list(trace, modelB)
assert set(vars_in_trace) == {a}
```

## Next Steps


---

*Source: test_forward.py:2084 | Complexity: Advanced | Last updated: 2026-05-18*