# How To: Truncation Discrete Random

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test truncation discrete random

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

### Step 1: Assign p = 0.2

```python
p = 0.2
```

**Verification:**
```python
assert isinstance(xt.owner.op, TruncatedRV)
```

### Step 2: Assign geometric_op = value

```python
geometric_op = icdf_geometric if op_type == 'icdf' else rejection_geometric
```

**Verification:**
```python
assert np.all(xt_draws >= lower)
```

### Step 3: Assign x = geometric_op(...)

```python
x = geometric_op(p, name='x', size=500)
```

**Verification:**
```python
assert np.all(xt_draws <= upper)
```

### Step 4: Assign xt = Truncated.dist(...)

```python
xt = Truncated.dist(x, lower=lower, upper=upper)
```

**Verification:**
```python
assert np.any(xt_draws == max(1, lower))
```

### Step 5: Assign xt_draws = draw(...)

```python
xt_draws = draw(xt)
```

**Verification:**
```python
assert np.any(xt_draws == upper)
```

### Step 6: Assign xt = Truncated.dist(...)

```python
xt = Truncated.dist(x, lower=lower, upper=upper, max_n_steps=3)
```

**Verification:**
```python
assert np.all(xt_draws >= lower)
```

### Step 7: Assign xt_draws = draw(...)

```python
xt_draws = draw(xt)
```

**Verification:**
```python
assert np.all(xt_draws <= upper)
```

### Step 8: Call draw()

```python
draw(xt, random_seed=2297228)
```

**Verification:**
```python
assert np.any(xt_draws == max(1, lower))
```


## Complete Example

```python
# Setup
# Fixtures: op_type, lower, upper

# Workflow
p = 0.2
geometric_op = icdf_geometric if op_type == 'icdf' else rejection_geometric
x = geometric_op(p, name='x', size=500)
xt = Truncated.dist(x, lower=lower, upper=upper)
assert isinstance(xt.owner.op, TruncatedRV)
xt_draws = draw(xt)
assert np.all(xt_draws >= lower)
assert np.all(xt_draws <= upper)
assert np.any(xt_draws == max(1, lower))
if upper != np.inf:
    assert np.any(xt_draws == upper)
xt = Truncated.dist(x, lower=lower, upper=upper, max_n_steps=3)
if op_type == 'icdf':
    xt_draws = draw(xt)
    assert np.all(xt_draws >= lower)
    assert np.all(xt_draws <= upper)
    assert np.any(xt_draws == max(1, lower))
    if upper != np.inf:
        assert np.any(xt_draws == upper)
else:
    with pytest.raises(TruncationError, match='^Truncation did not converge'):
        draw(xt, random_seed=2297228)
```

## Next Steps


---

*Source: test_truncated.py:243 | Complexity: Advanced | Last updated: 2026-05-18*