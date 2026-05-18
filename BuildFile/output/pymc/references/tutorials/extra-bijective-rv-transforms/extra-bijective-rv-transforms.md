# How To: Extra Bijective Rv Transforms

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test extra bijective rv transforms

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `scipy`
- `scipy.special`
- `pytensor.graph.basic`
- `pymc.distributions.continuous`
- `pymc.distributions.discrete`
- `pymc.logprob.basic`
- `pymc.logprob.transforms`
- `pymc.logprob.utils`
- `pymc.testing`
- `tests.distributions.test_transform`

**Setup Required:**
```python
# Fixtures: pt_transform, transform
```

## Step-by-Step Guide

### Step 1: Assign base_rv = pt.random.normal(...)

```python
base_rv = pt.random.normal(0.5, 1, name='base_rv')
```

### Step 2: Assign rv = pt_transform(...)

```python
rv = pt_transform(base_rv)
```

### Step 3: Assign vv = rv.clone(...)

```python
vv = rv.clone()
```

### Step 4: Assign rv_logp = logp(...)

```python
rv_logp = logp(rv, vv)
```

### Step 5: Assign expected_logp = value

```python
expected_logp = logp(base_rv, transform.backward(vv)) + transform.log_jac_det(vv)
```

### Step 6: Assign vv_test = np.array(...)

```python
vv_test = np.array(0.25)
```

### Step 7: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(rv_logp.eval({vv: vv_test}), np.nan_to_num(expected_logp.eval({vv: vv_test}), nan=-np.inf))
```


## Complete Example

```python
# Setup
# Fixtures: pt_transform, transform

# Workflow
base_rv = pt.random.normal(0.5, 1, name='base_rv')
rv = pt_transform(base_rv)
vv = rv.clone()
rv_logp = logp(rv, vv)
expected_logp = logp(base_rv, transform.backward(vv)) + transform.log_jac_det(vv)
vv_test = np.array(0.25)
np.testing.assert_allclose(rv_logp.eval({vv: vv_test}), np.nan_to_num(expected_logp.eval({vv: vv_test}), nan=-np.inf))
```

## Next Steps


---

*Source: test_transforms.py:535 | Complexity: Intermediate | Last updated: 2026-05-18*