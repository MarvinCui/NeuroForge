# How To: Get Value Vars From User Vars

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test get value vars from user vars

## Prerequisites

**Required Modules:**
- `re`
- `arviz`
- `numpy`
- `pytest`
- `xarray`
- `cachetools`
- `pymc`
- `pymc.distributions.transforms`
- `pymc.util`


## Step-by-Step Guide

### Step 1: Assign x1_value = value

```python
x1_value = model1.rvs_to_values[x1]
```

**Verification:**
```python
assert get_value_vars_from_user_vars([x1, y1], model1) == [x1_value, y1_value]
```

### Step 2: Assign y1_value = value

```python
y1_value = model1.rvs_to_values[y1]
```

**Verification:**
```python
assert get_value_vars_from_user_vars([x1], model1) == [x1_value]
```

### Step 3: Assign prefix = 'The following variables are not random variables in the model:'

```python
prefix = 'The following variables are not random variables in the model:'
```

**Verification:**
```python
assert get_value_vars_from_user_vars(x1_value, model1) == [x1_value]
```

### Step 4: Assign x1 = pm.Normal(...)

```python
x1 = pm.Normal('x1', mu=0, sigma=1)
```

**Verification:**
```python
assert get_value_vars_from_user_vars([], model1) == []
```

### Step 5: Assign y1 = pm.Normal(...)

```python
y1 = pm.Normal('y1', mu=0, sigma=1)
```

### Step 6: Assign x2 = pm.Normal(...)

```python
x2 = pm.Normal('x2', mu=0, sigma=1)
```

### Step 7: Assign y2 = pm.Normal(...)

```python
y2 = pm.Normal('y2', mu=0, sigma=1)
```

### Step 8: Assign det2 = pm.Deterministic(...)

```python
det2 = pm.Deterministic('det2', x2 + y2)
```

### Step 9: Call get_value_vars_from_user_vars()

```python
get_value_vars_from_user_vars([x2, y2], model1)
```

### Step 10: Call get_value_vars_from_user_vars()

```python
get_value_vars_from_user_vars([x2, y1], model1)
```

### Step 11: Call get_value_vars_from_user_vars()

```python
get_value_vars_from_user_vars([x2], model1)
```

### Step 12: Call get_value_vars_from_user_vars()

```python
get_value_vars_from_user_vars([det2], model2)
```


## Complete Example

```python
# Workflow
with pm.Model() as model1:
    x1 = pm.Normal('x1', mu=0, sigma=1)
    y1 = pm.Normal('y1', mu=0, sigma=1)
x1_value = model1.rvs_to_values[x1]
y1_value = model1.rvs_to_values[y1]
assert get_value_vars_from_user_vars([x1, y1], model1) == [x1_value, y1_value]
assert get_value_vars_from_user_vars([x1], model1) == [x1_value]
assert get_value_vars_from_user_vars(x1_value, model1) == [x1_value]
assert get_value_vars_from_user_vars([], model1) == []
with pm.Model() as model2:
    x2 = pm.Normal('x2', mu=0, sigma=1)
    y2 = pm.Normal('y2', mu=0, sigma=1)
    det2 = pm.Deterministic('det2', x2 + y2)
prefix = 'The following variables are not random variables in the model:'
with pytest.raises(ValueError, match=f"{prefix} \\['x2', 'y2'\\]"):
    get_value_vars_from_user_vars([x2, y2], model1)
with pytest.raises(ValueError, match=f"{prefix} \\['x2'\\]"):
    get_value_vars_from_user_vars([x2, y1], model1)
with pytest.raises(ValueError, match=f"{prefix} \\['x2'\\]"):
    get_value_vars_from_user_vars([x2], model1)
with pytest.raises(ValueError, match=f"{prefix} \\['det2'\\]"):
    get_value_vars_from_user_vars([det2], model2)
```

## Next Steps


---

*Source: test_util.py:228 | Complexity: Advanced | Last updated: 2026-05-18*