# How To: Hierarchical Value Transform

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: This model requires rv-value replacements in the backward transformation of
the value var `x`

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

### Step 1: '\n    This model requires rv-value replacements in the backward transformation of\n    the value var `x`\n    '

```python
'\n    This model requires rv-value replacements in the backward transformation of\n    the value var `x`\n    '
```

**Verification:**
```python
assert_no_rvs(logp_combined)
```

### Step 2: Assign lower_rv = pt.random.uniform(...)

```python
lower_rv = pt.random.uniform(0, 1, name='lower')
```

**Verification:**
```python
assert not np.isinf(logp_combined.eval({lower: -10, upper: 20, x: -20}))
```

### Step 3: Assign upper_rv = pt.random.uniform(...)

```python
upper_rv = pt.random.uniform(9, 10, name='upper')
```

### Step 4: Assign x_rv = pt.random.uniform(...)

```python
x_rv = pt.random.uniform(lower_rv, upper_rv, name='x')
```

### Step 5: Assign lower = lower_rv.clone(...)

```python
lower = lower_rv.clone()
```

### Step 6: Assign upper = upper_rv.clone(...)

```python
upper = upper_rv.clone()
```

### Step 7: Assign x = x_rv.clone(...)

```python
x = x_rv.clone()
```

### Step 8: Assign transform_rewrite = TransformValuesRewrite(...)

```python
transform_rewrite = TransformValuesRewrite({lower: _default_transform(lower_rv.owner.op, lower_rv), upper: _default_transform(upper_rv.owner.op, upper_rv), x: _default_transform(x_rv.owner.op, x_rv)})
```

### Step 9: Assign logp = conditional_logp(...)

```python
logp = conditional_logp({lower_rv: lower, upper_rv: upper, x_rv: x}, extra_rewrites=transform_rewrite)
```

### Step 10: Assign logp_combined = pt.sum(...)

```python
logp_combined = pt.sum([pt.sum(factor) for factor in logp.values()])
```

### Step 11: Call assert_no_rvs()

```python
assert_no_rvs(logp_combined)
```

**Verification:**
```python
assert not np.isinf(logp_combined.eval({lower: -10, upper: 20, x: -20}))
```


## Complete Example

```python
# Workflow
'\n    This model requires rv-value replacements in the backward transformation of\n    the value var `x`\n    '
lower_rv = pt.random.uniform(0, 1, name='lower')
upper_rv = pt.random.uniform(9, 10, name='upper')
x_rv = pt.random.uniform(lower_rv, upper_rv, name='x')
lower = lower_rv.clone()
upper = upper_rv.clone()
x = x_rv.clone()
transform_rewrite = TransformValuesRewrite({lower: _default_transform(lower_rv.owner.op, lower_rv), upper: _default_transform(upper_rv.owner.op, upper_rv), x: _default_transform(x_rv.owner.op, x_rv)})
logp = conditional_logp({lower_rv: lower, upper_rv: upper, x_rv: x}, extra_rewrites=transform_rewrite)
logp_combined = pt.sum([pt.sum(factor) for factor in logp.values()])
assert_no_rvs(logp_combined)
assert not np.isinf(logp_combined.eval({lower: -10, upper: 20, x: -20}))
```

## Next Steps


---

*Source: test_transform_value.py:319 | Complexity: Advanced | Last updated: 2026-05-18*