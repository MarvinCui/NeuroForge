# How To: Truncation Continuous Random

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test truncation continuous random

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `scipy`
- `pytensor.scalar`
- `pytensor.scan.op`
- `pytensor.tensor.random.basic`
- `pytensor.tensor.random.type`
- `pymc`
- `pymc.distributions`
- `pymc.distributions.shape_utils`
- `pymc.distributions.transforms`
- `pymc.distributions.truncated`
- `pymc.exceptions`
- `pymc.logprob.abstract`
- `pymc.logprob.basic`
- `pymc.logprob.transforms`
- `pymc.logprob.utils`
- `pymc.pytensorf`
- `pymc.testing`

**Setup Required:**
```python
# Fixtures: op_type, lower, upper, scalar, custom_dist
```

## Step-by-Step Guide

### Step 1: Assign loc = 0.15

```python
loc = 0.15
```

**Verification:**
```python
assert isinstance(xt.owner.op, TruncatedRV)
```

### Step 2: Assign scale = 10

```python
scale = 10
```

**Verification:**
```python
assert xt.type.dtype == x.type.dtype
```

### Step 3: Assign x = normal_op(...)

```python
x = normal_op(loc, scale, name='x', size=() if scalar else (100,))
```

**Verification:**
```python
assert np.all(xt_draws >= lower)
```

### Step 4: Assign xt = Truncated.dist(...)

```python
xt = Truncated.dist(x, lower=lower, upper=upper)
```

**Verification:**
```python
assert np.all(xt_draws <= upper)
```

### Step 5: Assign xt_draws = draw(...)

```python
xt_draws = draw(xt, draws=5)
```

**Verification:**
```python
assert np.unique(xt_draws).size == xt_draws.size
```

### Step 6: Assign ref_xt = scipy.stats.truncnorm(...)

```python
ref_xt = scipy.stats.truncnorm((lower - loc) / scale, (upper - loc) / scale, loc, scale)
```

**Verification:**
```python
assert scipy.stats.cramervonmises(xt_draws.ravel(), ref_xt.cdf).pvalue > 0.001
```

### Step 7: Assign xt = Truncated.dist(...)

```python
xt = Truncated.dist(x, lower=lower, upper=upper, max_n_steps=1)
```

**Verification:**
```python
assert np.all(xt_draws >= lower)
```

### Step 8: Assign normal_op = value

```python
normal_op = icdf_normal_customdist if op_type == 'icdf' else rejection_normal_customdist
```

**Verification:**
```python
assert np.all(xt_draws <= upper)
```

### Step 9: Assign normal_op = value

```python
normal_op = icdf_normal if op_type == 'icdf' else rejection_normal
```

**Verification:**
```python
assert np.unique(xt_draws).size == xt_draws.size
```

### Step 10: Assign xt_draws = draw(...)

```python
xt_draws = draw(xt)
```

**Verification:**
```python
assert np.all(xt_draws >= lower)
```

### Step 11: Call draw()

```python
draw(xt, draws=100 if scalar else 1)
```


## Complete Example

```python
# Setup
# Fixtures: op_type, lower, upper, scalar, custom_dist

# Workflow
loc = 0.15
scale = 10
if custom_dist:
    normal_op = icdf_normal_customdist if op_type == 'icdf' else rejection_normal_customdist
else:
    normal_op = icdf_normal if op_type == 'icdf' else rejection_normal
x = normal_op(loc, scale, name='x', size=() if scalar else (100,))
xt = Truncated.dist(x, lower=lower, upper=upper)
assert isinstance(xt.owner.op, TruncatedRV)
assert xt.type.dtype == x.type.dtype
xt_draws = draw(xt, draws=5)
assert np.all(xt_draws >= lower)
assert np.all(xt_draws <= upper)
assert np.unique(xt_draws).size == xt_draws.size
ref_xt = scipy.stats.truncnorm((lower - loc) / scale, (upper - loc) / scale, loc, scale)
assert scipy.stats.cramervonmises(xt_draws.ravel(), ref_xt.cdf).pvalue > 0.001
xt = Truncated.dist(x, lower=lower, upper=upper, max_n_steps=1)
if op_type == 'icdf':
    xt_draws = draw(xt)
    assert np.all(xt_draws >= lower)
    assert np.all(xt_draws <= upper)
    assert np.unique(xt_draws).size == xt_draws.size
else:
    with pytest.raises(TruncationError, match='^Truncation did not converge'):
        draw(xt, draws=100 if scalar else 1)
```

## Next Steps


---

*Source: test_truncated.py:138 | Complexity: Advanced | Last updated: 2026-05-18*