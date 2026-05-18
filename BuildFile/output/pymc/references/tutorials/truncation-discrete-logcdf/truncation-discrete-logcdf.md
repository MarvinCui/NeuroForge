# How To: Truncation Discrete Logcdf

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test truncation discrete logcdf

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
# Fixtures: op_type, lower, upper
```

## Step-by-Step Guide

### Step 1: Assign p = 0.7

```python
p = 0.7
```

**Verification:**
```python
assert isinstance(xt.owner.op, TruncatedRV)
```

### Step 2: Assign op = value

```python
op = icdf_geometric if op_type == 'icdf' else rejection_geometric
```

**Verification:**
```python
assert np.isclose(xt_logcdf_fn(test_xt_v), ref_xt_logcdf(test_xt_v))
```

### Step 3: Assign x = op(...)

```python
x = op(p, name='x')
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

### Step 6: Assign xt_logcdf_fn = pytensor.function(...)

```python
xt_logcdf_fn = pytensor.function([xt_vv], logcdf(xt, xt_vv))
```

### Step 7: Assign ref_xt = scipy.stats.geom(...)

```python
ref_xt = scipy.stats.geom(p)
```

### Step 8: Assign log_norm = np.log(...)

```python
log_norm = np.log(ref_xt.cdf(upper) - ref_xt.cdf(lower - 1))
```

### Step 9: Assign test_xt_v = value

```python
test_xt_v = bound + offset
```

**Verification:**
```python
assert np.isclose(xt_logcdf_fn(test_xt_v), ref_xt_logcdf(test_xt_v))
```


## Complete Example

```python
# Setup
# Fixtures: op_type, lower, upper

# Workflow
p = 0.7
op = icdf_geometric if op_type == 'icdf' else rejection_geometric
x = op(p, name='x')
xt = Truncated.dist(x, lower=lower, upper=upper)
assert isinstance(xt.owner.op, TruncatedRV)
xt_vv = xt.clone()
xt_logcdf_fn = pytensor.function([xt_vv], logcdf(xt, xt_vv))
ref_xt = scipy.stats.geom(p)
log_norm = np.log(ref_xt.cdf(upper) - ref_xt.cdf(lower - 1))

def ref_xt_logcdf(value):
    if value < lower:
        return -np.inf
    elif value > upper:
        return 0.0
    return np.log(ref_xt.cdf(value) - ref_xt.cdf(lower - 1)) - log_norm
for bound in (lower, upper):
    if np.isinf(bound):
        continue
    for offset in (-1, 0, 1):
        test_xt_v = bound + offset
        assert np.isclose(xt_logcdf_fn(test_xt_v), ref_xt_logcdf(test_xt_v))
```

## Next Steps


---

*Source: test_truncated.py:310 | Complexity: Advanced | Last updated: 2026-05-18*