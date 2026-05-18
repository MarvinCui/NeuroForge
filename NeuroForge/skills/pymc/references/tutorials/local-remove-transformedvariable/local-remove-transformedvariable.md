# How To: Local Remove Transformedvariable

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test local remove TransformedVariable

## Prerequisites

**Required Modules:**
- `pytensor.tensor`
- `pytensor.graph`
- `pytensor.graph.rewriting.basic`
- `pytensor.graph.rewriting.utils`
- `pytensor.tensor.elemwise`
- `pytensor.tensor.subtensor`
- `pymc.distributions.transforms`
- `pymc.logprob.basic`
- `pymc.logprob.rewriting`
- `pymc.logprob.transform_value`
- `pymc.logprob.utils`


## Step-by-Step Guide

### Step 1: Assign p_rv = pt.random.beta(...)

```python
p_rv = pt.random.beta(1, 1, name='p')
```

**Verification:**
```python
assert not any((isinstance(v.owner.op, TransformedValue) for v in ancestors([p_logp]) if v.owner))
```

### Step 2: Assign p_vv = p_rv.clone(...)

```python
p_vv = p_rv.clone()
```

### Step 3: Assign tr = TransformValuesRewrite(...)

```python
tr = TransformValuesRewrite({p_vv: logodds})
```

### Step 4: Assign unknown = conditional_logp.values(...)

```python
[p_logp] = conditional_logp({p_rv: p_vv}, extra_rewrites=tr).values()
```

**Verification:**
```python
assert not any((isinstance(v.owner.op, TransformedValue) for v in ancestors([p_logp]) if v.owner))
```


## Complete Example

```python
# Workflow
p_rv = pt.random.beta(1, 1, name='p')
p_vv = p_rv.clone()
tr = TransformValuesRewrite({p_vv: logodds})
[p_logp] = conditional_logp({p_rv: p_vv}, extra_rewrites=tr).values()
assert not any((isinstance(v.owner.op, TransformedValue) for v in ancestors([p_logp]) if v.owner))
```

## Next Steps


---

*Source: test_rewriting.py:94 | Complexity: Intermediate | Last updated: 2026-05-18*