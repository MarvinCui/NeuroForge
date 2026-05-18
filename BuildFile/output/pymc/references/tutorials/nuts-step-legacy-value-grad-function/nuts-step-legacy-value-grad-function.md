# How To: Nuts Step Legacy Value Grad Function

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test nuts step legacy value grad function

## Prerequisites

**Required Modules:**
- `logging`
- `warnings`
- `numpy`
- `pytensor.tensor`
- `pytest`
- `pymc`
- `pymc.exceptions`
- `pymc.pytensorf`
- `pymc.step_methods.hmc`
- `tests`
- `tests.helpers`


## Step-by-Step Guide

### Step 1: Assign legacy_value_grad_fn = m.logp_dlogp_function(...)

```python
legacy_value_grad_fn = m.logp_dlogp_function(ravel_inputs=False, mode='FAST_COMPILE')
```

**Verification:**
```python
assert np.all(new_ip['x'] != ip['x'])
```

### Step 2: Call legacy_value_grad_fn.set_extra_values()

```python
legacy_value_grad_fn.set_extra_values({})
```

**Verification:**
```python
assert np.all(new_ip['y'] != ip['y'])
```

### Step 3: Assign nuts = NUTS(...)

```python
nuts = NUTS(model=m, logp_dlogp_func=legacy_value_grad_fn)
```

### Step 4: Assign unknown = nuts._logp_dlogp_func(...)

```python
logp, dlogp = nuts._logp_dlogp_func([np.zeros((2,)), np.zeros((3, 2))])
```

### Step 5: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(dlogp, np.zeros(8))
```

### Step 6: Assign ip = m.initial_point(...)

```python
ip = m.initial_point()
```

### Step 7: Assign unknown = nuts.step(...)

```python
new_ip, _ = nuts.step(ip)
```

**Verification:**
```python
assert np.all(new_ip['x'] != ip['x'])
```

### Step 8: Assign x = pm.Normal(...)

```python
x = pm.Normal('x', shape=(2,))
```

### Step 9: Assign y = pm.Normal(...)

```python
y = pm.Normal('y', x, shape=(3, 2))
```


## Complete Example

```python
# Workflow
with pm.Model() as m:
    x = pm.Normal('x', shape=(2,))
    y = pm.Normal('y', x, shape=(3, 2))
legacy_value_grad_fn = m.logp_dlogp_function(ravel_inputs=False, mode='FAST_COMPILE')
legacy_value_grad_fn.set_extra_values({})
nuts = NUTS(model=m, logp_dlogp_func=legacy_value_grad_fn)
logp, dlogp = nuts._logp_dlogp_func([np.zeros((2,)), np.zeros((3, 2))])
np.testing.assert_allclose(dlogp, np.zeros(8))
ip = m.initial_point()
new_ip, _ = nuts.step(ip)
assert np.all(new_ip['x'] != ip['x'])
assert np.all(new_ip['y'] != ip['y'])
```

## Next Steps


---

*Source: test_nuts.py:212 | Complexity: Advanced | Last updated: 2026-05-18*