# How To: Persist Inputs

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Make sure we don't unnecessarily clone variables.

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

### Step 1: "Make sure we don't unnecessarily clone variables."

```python
"Make sure we don't unnecessarily clone variables."
```

**Verification:**
```python
assert x in ancestors([logp_combined])
```

### Step 2: Assign x = pt.scalar(...)

```python
x = pt.scalar('x')
```

**Verification:**
```python
assert y_vv in ancestors([logp_2_combined])
```

### Step 3: Assign beta_rv = pt.random.normal(...)

```python
beta_rv = pt.random.normal(0, 1, name='beta')
```

**Verification:**
```python
assert y_vv_2 in ancestors([logp_2_combined])
```

### Step 4: Assign Y_rv = pt.random.normal(...)

```python
Y_rv = pt.random.normal(beta_rv * x, 1, name='y')
```

**Verification:**
```python
assert y_vv in ancestors([logp_2_combined])
```

### Step 5: Assign beta_vv = beta_rv.type(...)

```python
beta_vv = beta_rv.type()
```

**Verification:**
```python
assert y_vv_2 in ancestors([logp_2_combined])
```

### Step 6: Assign y_vv = Y_rv.clone(...)

```python
y_vv = Y_rv.clone()
```

### Step 7: Assign logp = conditional_logp(...)

```python
logp = conditional_logp({beta_rv: beta_vv, Y_rv: y_vv})
```

### Step 8: Assign logp_combined = pt.sum(...)

```python
logp_combined = pt.sum([pt.sum(factor) for factor in logp.values()])
```

**Verification:**
```python
assert x in ancestors([logp_combined])
```

### Step 9: Assign y_vv_2 = value

```python
y_vv_2 = y_vv * 2
```

### Step 10: Assign logp_2 = conditional_logp(...)

```python
logp_2 = conditional_logp({beta_rv: beta_vv, Y_rv: y_vv_2})
```

### Step 11: Assign logp_2_combined = pt.sum(...)

```python
logp_2_combined = pt.sum([pt.sum(factor) for factor in logp_2.values()])
```

**Verification:**
```python
assert y_vv in ancestors([logp_2_combined])
```

### Step 12: Assign y_vv = pt.random.normal(...)

```python
y_vv = pt.random.normal(name='y_vv2')
```

### Step 13: Assign y_vv_2 = value

```python
y_vv_2 = y_vv * 2
```

### Step 14: Assign logp_2 = conditional_logp(...)

```python
logp_2 = conditional_logp({beta_rv: beta_vv, Y_rv: y_vv_2})
```

### Step 15: Assign logp_2_combined = pt.sum(...)

```python
logp_2_combined = pt.sum([pt.sum(factor) for factor in logp_2.values()])
```

**Verification:**
```python
assert y_vv in ancestors([logp_2_combined])
```


## Complete Example

```python
# Workflow
"Make sure we don't unnecessarily clone variables."
x = pt.scalar('x')
beta_rv = pt.random.normal(0, 1, name='beta')
Y_rv = pt.random.normal(beta_rv * x, 1, name='y')
beta_vv = beta_rv.type()
y_vv = Y_rv.clone()
logp = conditional_logp({beta_rv: beta_vv, Y_rv: y_vv})
logp_combined = pt.sum([pt.sum(factor) for factor in logp.values()])
assert x in ancestors([logp_combined])
y_vv_2 = y_vv * 2
logp_2 = conditional_logp({beta_rv: beta_vv, Y_rv: y_vv_2})
logp_2_combined = pt.sum([pt.sum(factor) for factor in logp_2.values()])
assert y_vv in ancestors([logp_2_combined])
assert y_vv_2 in ancestors([logp_2_combined])
y_vv = pt.random.normal(name='y_vv2')
y_vv_2 = y_vv * 2
logp_2 = conditional_logp({beta_rv: beta_vv, Y_rv: y_vv_2})
logp_2_combined = pt.sum([pt.sum(factor) for factor in logp_2.values()])
assert y_vv in ancestors([logp_2_combined])
assert y_vv_2 in ancestors([logp_2_combined])
```

## Next Steps


---

*Source: test_basic.py:174 | Complexity: Advanced | Last updated: 2026-05-18*