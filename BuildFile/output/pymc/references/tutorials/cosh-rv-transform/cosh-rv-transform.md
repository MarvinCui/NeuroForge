# How To: Cosh Rv Transform

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test cosh rv transform

## Prerequisites

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


## Step-by-Step Guide

### Step 1: Assign base_rv = pt.random.normal(...)

```python
base_rv = pt.random.normal(0.5, 1, size=(2,), name='base_rv')
```

### Step 2: Assign rv = pt.cosh(...)

```python
rv = pt.cosh(base_rv)
```

### Step 3: Assign vv = rv.clone(...)

```python
vv = rv.clone()
```

### Step 4: Assign rv_logp = logp(...)

```python
rv_logp = logp(rv, vv)
```

### Step 5: Assign transform = CoshTransform(...)

```python
transform = CoshTransform()
```

### Step 6: Assign unknown = transform.backward(...)

```python
[back_neg, back_pos] = transform.backward(vv)
```

### Step 7: Assign expected_logp = value

```python
expected_logp = pt.logaddexp(logp(base_rv, back_neg), logp(base_rv, back_pos)) + transform.log_jac_det(vv)
```

### Step 8: Assign vv_test = np.array(...)

```python
vv_test = np.array([0.25, 1.5])
```

### Step 9: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(rv_logp.eval({vv: vv_test}), np.nan_to_num(expected_logp.eval({vv: vv_test}), nan=-np.inf))
```

### Step 10: Call logcdf()

```python
logcdf(rv, vv)
```

### Step 11: Call icdf()

```python
icdf(rv, vv)
```


## Complete Example

```python
# Workflow
base_rv = pt.random.normal(0.5, 1, size=(2,), name='base_rv')
rv = pt.cosh(base_rv)
vv = rv.clone()
rv_logp = logp(rv, vv)
with pytest.raises(NotImplementedError):
    logcdf(rv, vv)
with pytest.raises(NotImplementedError):
    icdf(rv, vv)
transform = CoshTransform()
[back_neg, back_pos] = transform.backward(vv)
expected_logp = pt.logaddexp(logp(base_rv, back_neg), logp(base_rv, back_pos)) + transform.log_jac_det(vv)
vv_test = np.array([0.25, 1.5])
np.testing.assert_allclose(rv_logp.eval({vv: vv_test}), np.nan_to_num(expected_logp.eval({vv: vv_test}), nan=-np.inf))
```

## Next Steps


---

*Source: test_transforms.py:578 | Complexity: Advanced | Last updated: 2026-05-18*