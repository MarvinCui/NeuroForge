# How To: Categorical

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test categorical

## Prerequisites

**Required Modules:**
- `math`
- `numpy`
- `pytensor.tensor`
- `pytest`
- `pytensor.xtensor`
- `pymc.distributions`
- `pymc`
- `pymc.dims`
- `tests.dims.utils`


## Step-by-Step Guide

### Step 1: Assign coords = value

```python
coords = {'a': range(3), 'b': range(4)}
```

**Verification:**
```python
assert_equivalent_random_graph(model, reference_model)
```

### Step 2: Assign p = pt.as_tensor(...)

```python
p = pt.as_tensor([0.1, 0.2, 0.3, 0.4])
```

**Verification:**
```python
assert_equivalent_logp_graph(model, reference_model)
```

### Step 3: Assign logit_p = pt.as_tensor(...)

```python
logit_p = pt.as_tensor([0.0, 0.0, math.log(2), math.log(4)])
```

### Step 4: Assign p_xr = as_xtensor(...)

```python
p_xr = as_xtensor(p, dims=('b',))
```

### Step 5: Assign logit_p_xr = as_xtensor(...)

```python
logit_p_xr = as_xtensor(logit_p, dims=('b',))
```

### Step 6: Call assert_equivalent_random_graph()

```python
assert_equivalent_random_graph(model, reference_model)
```

### Step 7: Call assert_equivalent_logp_graph()

```python
assert_equivalent_logp_graph(model, reference_model)
```

### Step 8: Call Categorical()

```python
Categorical('x', p=p_xr, core_dims='b', dims=('a',))
```

### Step 9: Call Categorical()

```python
Categorical('y', logit_p=logit_p_xr, core_dims='b', dims=('a',))
```

### Step 10: Call regular_distributions.Categorical()

```python
regular_distributions.Categorical('x', p=p, dims=('a',))
```

### Step 11: Call regular_distributions.Categorical()

```python
regular_distributions.Categorical('y', logit_p=logit_p, dims=('a',))
```


## Complete Example

```python
# Workflow
coords = {'a': range(3), 'b': range(4)}
p = pt.as_tensor([0.1, 0.2, 0.3, 0.4])
logit_p = pt.as_tensor([0.0, 0.0, math.log(2), math.log(4)])
p_xr = as_xtensor(p, dims=('b',))
logit_p_xr = as_xtensor(logit_p, dims=('b',))
with Model(coords=coords) as model:
    Categorical('x', p=p_xr, core_dims='b', dims=('a',))
    Categorical('y', logit_p=logit_p_xr, core_dims='b', dims=('a',))
with Model(coords=coords) as reference_model:
    regular_distributions.Categorical('x', p=p, dims=('a',))
    regular_distributions.Categorical('y', logit_p=logit_p, dims=('a',))
assert_equivalent_random_graph(model, reference_model)
assert_equivalent_logp_graph(model, reference_model)
```

## Next Steps


---

*Source: test_vector.py:31 | Complexity: Advanced | Last updated: 2026-05-18*