# How To: Truncation Continuous Logp

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test truncation continuous logp

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
# Fixtures: op_type, lower, upper, custom_dist
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
assert np.isclose(xt_logp_fn(test_xt_v), ref_xt.logpdf(test_xt_v))
```

### Step 3: Assign x = op(...)

```python
x = op(loc, scale, name='x')
```

### Step 4: Assign xt = Truncated.dist(...)

```python
xt = Truncated.dist(x, lower=lower, upper=upper)
```

**Verification:**
```python
assert isinstance(xt.owner.op, TruncatedRV)
```

### Step 5: Assign xt_vv = xt.clone(...)

```python
xt_vv = xt.clone()
```

### Step 6: Assign xt_logp_fn = pytensor.function(...)

```python
xt_logp_fn = pytensor.function([xt_vv], logp(xt, xt_vv))
```

### Step 7: Assign ref_xt = scipy.stats.truncnorm(...)

```python
ref_xt = scipy.stats.truncnorm((lower - loc) / scale, (upper - loc) / scale, loc, scale)
```

### Step 8: Assign op = value

```python
op = icdf_normal_customdist if op_type == 'icdf' else rejection_normal_customdist
```

### Step 9: Assign op = value

```python
op = icdf_normal if op_type == 'icdf' else rejection_normal
```

### Step 10: Assign test_xt_v = value

```python
test_xt_v = bound + offset
```

**Verification:**
```python
assert np.isclose(xt_logp_fn(test_xt_v), ref_xt.logpdf(test_xt_v))
```


## Complete Example

```python
# Setup
# Fixtures: op_type, lower, upper, custom_dist

# Workflow
loc = 0.15
scale = 10
if custom_dist:
    op = icdf_normal_customdist if op_type == 'icdf' else rejection_normal_customdist
else:
    op = icdf_normal if op_type == 'icdf' else rejection_normal
x = op(loc, scale, name='x')
xt = Truncated.dist(x, lower=lower, upper=upper)
assert isinstance(xt.owner.op, TruncatedRV)
xt_vv = xt.clone()
xt_logp_fn = pytensor.function([xt_vv], logp(xt, xt_vv))
ref_xt = scipy.stats.truncnorm((lower - loc) / scale, (upper - loc) / scale, loc, scale)
for bound in (lower, upper):
    if np.isinf(bound):
        return
    for offset in (-1, 0, 1):
        test_xt_v = bound + offset
        assert np.isclose(xt_logp_fn(test_xt_v), ref_xt.logpdf(test_xt_v))
```

## Next Steps


---

*Source: test_truncated.py:180 | Complexity: Advanced | Last updated: 2026-05-18*