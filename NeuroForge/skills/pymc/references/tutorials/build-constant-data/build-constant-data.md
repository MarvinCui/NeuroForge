# How To: Build Constant Data

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test build constant data

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

### Step 1: Assign length_var = value

```python
length_var = model.dim_lengths['length_coord']
```

**Verification:**
```python
assert set(constant_data_same) == {x, length_var, value_var}
```

### Step 2: Assign value_var = value

```python
value_var = model.dim_lengths['value_coord']
```

**Verification:**
```python
assert set(constant_data_diff) == {x}
```

### Step 3: Assign trace_constant_data = value

```python
trace_constant_data = {'x': np.array([1.0, 2.0, 3.0])}
```

**Verification:**
```python
assert x not in constant_data_no_x
```

### Step 4: Assign trace_coords_same = value

```python
trace_coords_same = {'length_coord': np.array([0]), 'value_coord': np.array([3])}
```

**Verification:**
```python
assert set(constant_data_no_x) == {length_var, value_var}
```

### Step 5: Assign constant_data_same = _build_constant_data(...)

```python
constant_data_same = _build_constant_data(trace_constant_data, trace_coords_same, model)
```

**Verification:**
```python
assert set(constant_data_same) == {x, length_var, value_var}
```

### Step 6: Assign trace_coords_diff = value

```python
trace_coords_diff = {'length_coord': np.array([0, 1]), 'value_coord': np.array([4])}
```

### Step 7: Assign constant_data_diff = _build_constant_data(...)

```python
constant_data_diff = _build_constant_data(trace_constant_data, trace_coords_diff, model)
```

**Verification:**
```python
assert set(constant_data_diff) == {x}
```

### Step 8: Assign constant_data_no_x = _build_constant_data(...)

```python
constant_data_no_x = _build_constant_data({}, trace_coords_same, model)
```

**Verification:**
```python
assert x not in constant_data_no_x
```

### Step 9: Call model.add_coord()

```python
model.add_coord('length_coord', length=1)
```

### Step 10: Call model.add_coord()

```python
model.add_coord('value_coord', values=(3,))
```

### Step 11: Assign x = pm.Data(...)

```python
x = pm.Data('x', np.array([1.0, 2.0, 3.0]))
```


## Complete Example

```python
# Workflow
with pm.Model() as model:
    model.add_coord('length_coord', length=1)
    model.add_coord('value_coord', values=(3,))
    x = pm.Data('x', np.array([1.0, 2.0, 3.0]))
length_var = model.dim_lengths['length_coord']
value_var = model.dim_lengths['value_coord']
trace_constant_data = {'x': np.array([1.0, 2.0, 3.0])}
trace_coords_same = {'length_coord': np.array([0]), 'value_coord': np.array([3])}
constant_data_same = _build_constant_data(trace_constant_data, trace_coords_same, model)
assert set(constant_data_same) == {x, length_var, value_var}
trace_coords_diff = {'length_coord': np.array([0, 1]), 'value_coord': np.array([4])}
constant_data_diff = _build_constant_data(trace_constant_data, trace_coords_diff, model)
assert set(constant_data_diff) == {x}
constant_data_no_x = _build_constant_data({}, trace_coords_same, model)
assert x not in constant_data_no_x
assert set(constant_data_no_x) == {length_var, value_var}
```

## Next Steps


---

*Source: test_forward.py:2058 | Complexity: Advanced | Last updated: 2026-05-18*