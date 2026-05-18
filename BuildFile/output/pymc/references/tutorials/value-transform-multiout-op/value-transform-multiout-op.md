# How To: Value Transform Multiout Op

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test value transform multiout op

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
# Fixtures: transform_x, transform_y, multiout_measurable_op
```

## Step-by-Step Guide

### Step 1: Assign unknown = multiout_measurable_op(...)

```python
x, y = multiout_measurable_op(1, 2)
```

### Step 2: Assign x.name = 'x'

```python
x.name = 'x'
```

### Step 3: Assign y.name = 'y'

```python
y.name = 'y'
```

### Step 4: Assign x_vv = x.clone(...)

```python
x_vv = x.clone()
```

### Step 5: Assign y_vv = y.clone(...)

```python
y_vv = y.clone()
```

### Step 6: Assign transform_rewrite = TransformValuesRewrite(...)

```python
transform_rewrite = TransformValuesRewrite({x_vv: LogTransform() if transform_x else None, y_vv: ExpTransform() if transform_y else None})
```

### Step 7: Assign logp = conditional_logp(...)

```python
logp = conditional_logp({x: x_vv, y: y_vv}, extra_rewrites=transform_rewrite)
```

### Step 8: Assign logp_combined = pt.sum(...)

```python
logp_combined = pt.sum([pt.sum(factor) for factor in logp.values()])
```

### Step 9: Assign x_vv_test = np.random.normal(...)

```python
x_vv_test = np.random.normal()
```

### Step 10: Assign y_vv_test = np.abs(...)

```python
y_vv_test = np.abs(np.random.normal())
```

### Step 11: Assign expected_logp = 0

```python
expected_logp = 0
```

### Step 12: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(logp_combined.eval({x_vv: x_vv_test, y_vv: y_vv_test}), expected_logp)
```


## Complete Example

```python
# Setup
# Fixtures: transform_x, transform_y, multiout_measurable_op

# Workflow
x, y = multiout_measurable_op(1, 2)
x.name = 'x'
y.name = 'y'
x_vv = x.clone()
y_vv = y.clone()
transform_rewrite = TransformValuesRewrite({x_vv: LogTransform() if transform_x else None, y_vv: ExpTransform() if transform_y else None})
logp = conditional_logp({x: x_vv, y: y_vv}, extra_rewrites=transform_rewrite)
logp_combined = pt.sum([pt.sum(factor) for factor in logp.values()])
x_vv_test = np.random.normal()
y_vv_test = np.abs(np.random.normal())
expected_logp = 0
if not transform_x:
    expected_logp += x_vv_test + 1
else:
    expected_logp += np.exp(x_vv_test) + 1 + x_vv_test
if not transform_y:
    expected_logp += y_vv_test + 2
else:
    expected_logp += np.log(y_vv_test) + 2 - np.log(y_vv_test)
np.testing.assert_allclose(logp_combined.eval({x_vv: x_vv_test, y_vv: y_vv_test}), expected_logp)
```

## Next Steps


---

*Source: test_transform_value.py:419 | Complexity: Advanced | Last updated: 2026-05-18*