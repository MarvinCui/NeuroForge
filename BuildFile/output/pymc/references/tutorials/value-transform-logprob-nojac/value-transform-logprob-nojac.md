# How To: Value Transform Logprob Nojac

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test value transform logprob nojac

## Prerequisites

- [ ] Setup code must be executed first

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

**Setup Required:**
```python
# Fixtures: use_jacobian
```

## Step-by-Step Guide

### Step 1: Assign X_rv = pt.random.halfnormal(...)

```python
X_rv = pt.random.halfnormal(0, 3, name='X')
```

### Step 2: Assign x_vv = X_rv.clone(...)

```python
x_vv = X_rv.clone()
```

### Step 3: Assign x_vv.name = 'x'

```python
x_vv.name = 'x'
```

### Step 4: Assign transform_rewrite = TransformValuesRewrite(...)

```python
transform_rewrite = TransformValuesRewrite({x_vv: log})
```

### Step 5: Assign tr_logp = conditional_logp(...)

```python
tr_logp = conditional_logp({X_rv: x_vv}, extra_rewrites=transform_rewrite, use_jacobian=use_jacobian)
```

### Step 6: Assign tr_logp_combined = pt.sum(...)

```python
tr_logp_combined = pt.sum([pt.sum(factor) for factor in tr_logp.values()])
```

### Step 7: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(tr_logp_combined.eval({x_vv: np.log(2.5)}), sp.stats.halfnorm(0, 3).logpdf(2.5) + (np.log(2.5) if use_jacobian else 0.0))
```


## Complete Example

```python
# Setup
# Fixtures: use_jacobian

# Workflow
X_rv = pt.random.halfnormal(0, 3, name='X')
x_vv = X_rv.clone()
x_vv.name = 'x'
transform_rewrite = TransformValuesRewrite({x_vv: log})
tr_logp = conditional_logp({X_rv: x_vv}, extra_rewrites=transform_rewrite, use_jacobian=use_jacobian)
tr_logp_combined = pt.sum([pt.sum(factor) for factor in tr_logp.values()])
np.testing.assert_allclose(tr_logp_combined.eval({x_vv: np.log(2.5)}), sp.stats.halfnorm(0, 3).logpdf(2.5) + (np.log(2.5) if use_jacobian else 0.0))
```

## Next Steps


---

*Source: test_transform_value.py:302 | Complexity: Intermediate | Last updated: 2026-05-18*