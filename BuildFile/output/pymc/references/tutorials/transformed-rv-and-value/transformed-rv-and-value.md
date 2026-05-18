# How To: Transformed Rv And Value

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test transformed rv and value

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

### Step 1: Assign y_rv = value

```python
y_rv = pt.random.halfnormal(-1, 1, name='base_rv') + 1
```

**Verification:**
```python
assert_no_rvs(logp_combined)
```

### Step 2: Assign y_rv.name = 'y'

```python
y_rv.name = 'y'
```

### Step 3: Assign y_vv = y_rv.clone(...)

```python
y_vv = y_rv.clone()
```

### Step 4: Assign transform_rewrite = TransformValuesRewrite(...)

```python
transform_rewrite = TransformValuesRewrite({y_vv: LogTransform()})
```

### Step 5: Assign logp = conditional_logp(...)

```python
logp = conditional_logp({y_rv: y_vv}, extra_rewrites=transform_rewrite)
```

### Step 6: Assign logp_combined = pt.sum(...)

```python
logp_combined = pt.sum([pt.sum(factor) for factor in logp.values()])
```

### Step 7: Call assert_no_rvs()

```python
assert_no_rvs(logp_combined)
```

### Step 8: Assign logp_fn = pytensor.function(...)

```python
logp_fn = pytensor.function([y_vv], logp_combined)
```

### Step 9: Assign y_test_val = value

```python
y_test_val = -5
```

### Step 10: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(logp_fn(y_test_val), sp.stats.halfnorm(0, 1).logpdf(np.exp(y_test_val)) + y_test_val)
```


## Complete Example

```python
# Workflow
y_rv = pt.random.halfnormal(-1, 1, name='base_rv') + 1
y_rv.name = 'y'
y_vv = y_rv.clone()
transform_rewrite = TransformValuesRewrite({y_vv: LogTransform()})
logp = conditional_logp({y_rv: y_vv}, extra_rewrites=transform_rewrite)
logp_combined = pt.sum([pt.sum(factor) for factor in logp.values()])
assert_no_rvs(logp_combined)
logp_fn = pytensor.function([y_vv], logp_combined)
y_test_val = -5
np.testing.assert_allclose(logp_fn(y_test_val), sp.stats.halfnorm(0, 1).logpdf(np.exp(y_test_val)) + y_test_val)
```

## Next Steps


---

*Source: test_transform_value.py:455 | Complexity: Advanced | Last updated: 2026-05-18*