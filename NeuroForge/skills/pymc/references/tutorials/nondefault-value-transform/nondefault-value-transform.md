# How To: Nondefault Value Transform

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test nondefault value transform

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

### Step 1: Assign loc_rv = pt.random.uniform(...)

```python
loc_rv = pt.random.uniform(-10, 10, name='loc')
```

### Step 2: Assign scale_rv = pt.random.uniform(...)

```python
scale_rv = pt.random.uniform(-1, 1, name='scale')
```

### Step 3: Assign x_rv = pt.random.normal(...)

```python
x_rv = pt.random.normal(loc_rv, scale_rv, name='x')
```

### Step 4: Assign loc = loc_rv.clone(...)

```python
loc = loc_rv.clone()
```

### Step 5: Assign scale = scale_rv.clone(...)

```python
scale = scale_rv.clone()
```

### Step 6: Assign x = x_rv.clone(...)

```python
x = x_rv.clone()
```

### Step 7: Assign transform_rewrite = TransformValuesRewrite(...)

```python
transform_rewrite = TransformValuesRewrite({loc: None, scale: LogOddsTransform(), x: LogTransform()})
```

### Step 8: Assign logp = conditional_logp(...)

```python
logp = conditional_logp({loc_rv: loc, scale_rv: scale, x_rv: x}, extra_rewrites=transform_rewrite)
```

### Step 9: Assign logp_combined = pt.sum(...)

```python
logp_combined = pt.sum([pt.sum(factor) for factor in logp.values()])
```

### Step 10: Assign loc_val = 0

```python
loc_val = 0
```

### Step 11: Assign scale_val_tr = value

```python
scale_val_tr = -1
```

### Step 12: Assign x_val_tr = value

```python
x_val_tr = -1
```

### Step 13: Assign scale_val = sp.special.expit(...)

```python
scale_val = sp.special.expit(scale_val_tr)
```

### Step 14: Assign x_val = np.exp(...)

```python
x_val = np.exp(x_val_tr)
```

### Step 15: Assign exp_logp = 0

```python
exp_logp = 0
```

### Step 16: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(logp_combined.eval({loc: loc_val, scale: scale_val_tr, x: x_val_tr}), exp_logp)
```


## Complete Example

```python
# Workflow
loc_rv = pt.random.uniform(-10, 10, name='loc')
scale_rv = pt.random.uniform(-1, 1, name='scale')
x_rv = pt.random.normal(loc_rv, scale_rv, name='x')
loc = loc_rv.clone()
scale = scale_rv.clone()
x = x_rv.clone()
transform_rewrite = TransformValuesRewrite({loc: None, scale: LogOddsTransform(), x: LogTransform()})
logp = conditional_logp({loc_rv: loc, scale_rv: scale, x_rv: x}, extra_rewrites=transform_rewrite)
logp_combined = pt.sum([pt.sum(factor) for factor in logp.values()])
loc_val = 0
scale_val_tr = -1
x_val_tr = -1
scale_val = sp.special.expit(scale_val_tr)
x_val = np.exp(x_val_tr)
exp_logp = 0
exp_logp += sp.stats.uniform(-10, 20).logpdf(loc_val)
exp_logp += sp.stats.uniform(-1, 2).logpdf(scale_val)
exp_logp += np.log(scale_val) + np.log1p(-scale_val)
exp_logp += sp.stats.norm(loc_val, scale_val).logpdf(x_val)
exp_logp += x_val_tr
np.testing.assert_allclose(logp_combined.eval({loc: loc_val, scale: scale_val_tr, x: x_val_tr}), exp_logp)
```

## Next Steps


---

*Source: test_transform_value.py:350 | Complexity: Advanced | Last updated: 2026-05-18*