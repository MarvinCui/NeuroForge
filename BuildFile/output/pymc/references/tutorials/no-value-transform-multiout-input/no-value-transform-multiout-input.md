# How To: No Value Transform Multiout Input

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Make sure that `Op`\s with multiple outputs are handled correctly.

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

### Step 1: 'Make sure that `Op`\\s with multiple outputs are handled correctly.'

```python
'Make sure that `Op`\\s with multiple outputs are handled correctly.'
```

### Step 2: Assign sd = value

```python
sd = pt.linalg.svd(pt.eye(1))[1][0]
```

### Step 3: Assign x_rv = pt.random.normal(...)

```python
x_rv = pt.random.normal(0, sd, name='x')
```

### Step 4: Assign x = x_rv.clone(...)

```python
x = x_rv.clone()
```

### Step 5: Assign transform_rewrite = TransformValuesRewrite(...)

```python
transform_rewrite = TransformValuesRewrite({x: None})
```

### Step 6: Assign logp = conditional_logp(...)

```python
logp = conditional_logp({x_rv: x}, extra_rewrites=transform_rewrite)
```

### Step 7: Assign logp_combined = pt.sum(...)

```python
logp_combined = pt.sum([pt.sum(factor) for factor in logp.values()])
```

### Step 8: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(logp_combined.eval({x: 1}), sp.stats.norm(0, 1).logpdf(1))
```


## Complete Example

```python
# Workflow
'Make sure that `Op`\\s with multiple outputs are handled correctly.'
sd = pt.linalg.svd(pt.eye(1))[1][0]
x_rv = pt.random.normal(0, sd, name='x')
x = x_rv.clone()
transform_rewrite = TransformValuesRewrite({x: None})
logp = conditional_logp({x_rv: x}, extra_rewrites=transform_rewrite)
logp_combined = pt.sum([pt.sum(factor) for factor in logp.values()])
np.testing.assert_allclose(logp_combined.eval({x: 1}), sp.stats.norm(0, 1).logpdf(1))
```

## Next Steps


---

*Source: test_transform_value.py:394 | Complexity: Advanced | Last updated: 2026-05-18*