# How To: Measurable Power Exponent With Constant Base

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test measurable power exponent with constant base

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

### Step 1: Assign x_rv_pow = pt.pow(...)

```python
x_rv_pow = pt.pow(2, pt.random.normal())
```

### Step 2: Assign x_rv_exp2 = pt.exp2(...)

```python
x_rv_exp2 = pt.exp2(pt.random.normal())
```

### Step 3: Assign x_vv_pow = x_rv_pow.clone(...)

```python
x_vv_pow = x_rv_pow.clone()
```

### Step 4: Assign x_vv_exp2 = x_rv_exp2.clone(...)

```python
x_vv_exp2 = x_rv_exp2.clone()
```

### Step 5: Assign x_logp_fn_pow = pytensor.function(...)

```python
x_logp_fn_pow = pytensor.function([x_vv_pow], pt.sum(logp(x_rv_pow, x_vv_pow)))
```

### Step 6: Assign x_logp_fn_exp2 = pytensor.function(...)

```python
x_logp_fn_exp2 = pytensor.function([x_vv_exp2], pt.sum(logp(x_rv_exp2, x_vv_exp2)))
```

### Step 7: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(x_logp_fn_pow(0.1), x_logp_fn_exp2(0.1))
```

### Step 8: Assign x_rv_neg = pt.pow(...)

```python
x_rv_neg = pt.pow(-2, pt.random.normal())
```

### Step 9: Assign x_vv_neg = x_rv_neg.clone(...)

```python
x_vv_neg = x_rv_neg.clone()
```

### Step 10: Call logp.eval()

```python
logp(x_rv_neg, x_vv_neg).eval({x_vv_neg: 1.5})
```


## Complete Example

```python
# Workflow
x_rv_pow = pt.pow(2, pt.random.normal())
x_rv_exp2 = pt.exp2(pt.random.normal())
x_vv_pow = x_rv_pow.clone()
x_vv_exp2 = x_rv_exp2.clone()
x_logp_fn_pow = pytensor.function([x_vv_pow], pt.sum(logp(x_rv_pow, x_vv_pow)))
x_logp_fn_exp2 = pytensor.function([x_vv_exp2], pt.sum(logp(x_rv_exp2, x_vv_exp2)))
np.testing.assert_allclose(x_logp_fn_pow(0.1), x_logp_fn_exp2(0.1))
x_rv_neg = pt.pow(-2, pt.random.normal())
x_vv_neg = x_rv_neg.clone()
with pytest.raises(ParameterValueError, match='base >= 0'):
    logp(x_rv_neg, x_vv_neg).eval({x_vv_neg: 1.5})
```

## Next Steps


---

*Source: test_transforms.py:634 | Complexity: Advanced | Last updated: 2026-05-18*