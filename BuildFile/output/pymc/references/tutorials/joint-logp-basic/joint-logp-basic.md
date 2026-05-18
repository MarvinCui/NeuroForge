# How To: Joint Logp Basic

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Make sure we can compute a log-likelihood for a hierarchical model with transforms.

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `scipy.stats.distributions`
- `pytensor.graph.basic`
- `pytensor.graph.traversal`
- `pytensor.tensor.random.op`
- `scipy`
- `pymc`
- `pymc.logprob.basic`
- `pymc.logprob.transforms`
- `pymc.logprob.utils`
- `pymc.testing`


## Step-by-Step Guide

### Step 1: 'Make sure we can compute a log-likelihood for a hierarchical model with transforms.'

```python
'Make sure we can compute a log-likelihood for a hierarchical model with transforms.'
```

**Verification:**
```python
assert m.rvs_to_transforms[a]
```

### Step 2: Assign a_value_var = value

```python
a_value_var = m.rvs_to_values[a]
```

**Verification:**
```python
assert m.rvs_to_transforms[b]
```

### Step 3: Assign b_value_var = value

```python
b_value_var = m.rvs_to_values[b]
```

**Verification:**
```python
assert_no_rvs(b_logp)
```

### Step 4: Assign c_value_var = value

```python
c_value_var = m.rvs_to_values[c]
```

**Verification:**
```python
assert b_value_var in res_ancestors
```

### Step 5: Assign unknown = transformed_conditional_logp(...)

```python
b_logp, = transformed_conditional_logp((b,), rvs_to_values=m.rvs_to_values, rvs_to_transforms=m.rvs_to_transforms)
```

**Verification:**
```python
assert c_value_var in res_ancestors
```

### Step 6: Call assert_no_rvs()

```python
assert_no_rvs(b_logp)
```

**Verification:**
```python
assert a_value_var in res_ancestors
```

### Step 7: Assign res_ancestors = list(...)

```python
res_ancestors = list(ancestors((b_logp,)))
```

**Verification:**
```python
assert b_value_var in res_ancestors
```

### Step 8: Assign a = pm.Uniform(...)

```python
a = pm.Uniform('a', 0.0, 1.0)
```

### Step 9: Assign c = pm.Normal(...)

```python
c = pm.Normal('c')
```

### Step 10: Assign b_l = value

```python
b_l = c * a + 2.0
```

### Step 11: Assign b = pm.Uniform(...)

```python
b = pm.Uniform('b', b_l, b_l + 1.0)
```


## Complete Example

```python
# Workflow
'Make sure we can compute a log-likelihood for a hierarchical model with transforms.'
with pm.Model() as m:
    a = pm.Uniform('a', 0.0, 1.0)
    c = pm.Normal('c')
    b_l = c * a + 2.0
    b = pm.Uniform('b', b_l, b_l + 1.0)
a_value_var = m.rvs_to_values[a]
assert m.rvs_to_transforms[a]
b_value_var = m.rvs_to_values[b]
assert m.rvs_to_transforms[b]
c_value_var = m.rvs_to_values[c]
b_logp, = transformed_conditional_logp((b,), rvs_to_values=m.rvs_to_values, rvs_to_transforms=m.rvs_to_transforms)
assert_no_rvs(b_logp)
res_ancestors = list(ancestors((b_logp,)))
assert b_value_var in res_ancestors
assert c_value_var in res_ancestors
assert a_value_var in res_ancestors
```

## Next Steps


---

*Source: test_basic.py:231 | Complexity: Advanced | Last updated: 2026-05-18*