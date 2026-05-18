# How To: Original Values Output Dict

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that the original unconstrained value variable appears an the key of
the logprob factor

## Prerequisites

**Required Modules:**
- `gc`
- `operator`
- `numpy`
- `pytensor`
- `pytest`
- `scipy`
- `numdifftools`
- `pytensor`
- `pytensor`
- `pytensor.compile.builders`
- `pytensor.graph`
- `pytensor.graph.basic`
- `pymc`
- `pymc.distributions.transforms`
- `pymc.logprob`
- `pymc.logprob.abstract`
- `pymc.logprob.transform_value`
- `pymc.logprob.transforms`
- `pymc.testing`
- `tests.logprob.test_transforms`
- `pymc.model.transform.optimization`


## Step-by-Step Guide

### Step 1: '\n    Test that the original unconstrained value variable appears an the key of\n    the logprob factor\n    '

```python
'\n    Test that the original unconstrained value variable appears an the key of\n    the logprob factor\n    '
```

**Verification:**
```python
assert p_vv in logp_dict
```

### Step 2: Assign p_rv = pt.random.beta(...)

```python
p_rv = pt.random.beta(1, 1, name='p')
```

### Step 3: Assign p_vv = p_rv.clone(...)

```python
p_vv = p_rv.clone()
```

### Step 4: Assign tr = TransformValuesRewrite(...)

```python
tr = TransformValuesRewrite({p_vv: logodds})
```

### Step 5: Assign logp_dict = conditional_logp(...)

```python
logp_dict = conditional_logp({p_rv: p_vv}, extra_rewrites=tr)
```

**Verification:**
```python
assert p_vv in logp_dict
```


## Complete Example

```python
# Workflow
'\n    Test that the original unconstrained value variable appears an the key of\n    the logprob factor\n    '
p_rv = pt.random.beta(1, 1, name='p')
p_vv = p_rv.clone()
tr = TransformValuesRewrite({p_vv: logodds})
logp_dict = conditional_logp({p_rv: p_vv}, extra_rewrites=tr)
assert p_vv in logp_dict
```

## Next Steps


---

*Source: test_transform_value.py:72 | Complexity: Intermediate | Last updated: 2026-05-18*