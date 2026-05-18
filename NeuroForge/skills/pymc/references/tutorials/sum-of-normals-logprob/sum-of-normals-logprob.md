# How To: Sum Of Normals Logprob

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test sum of normals logprob

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `pytensor`
- `pymc.logprob.basic`

**Setup Required:**
```python
# Fixtures: axis
```

## Step-by-Step Guide

### Step 1: Assign mu = pt.constant(...)

```python
mu = pt.constant([[1.0, 2.0, 3.0], [0.5, 1.5, 2.5]])
```

### Step 2: Assign sigma = pt.constant(...)

```python
sigma = pt.constant([[1.0, 2.0, 3.0], [1.5, 2.5, 3.5]])
```

### Step 3: Assign x_rv = pt.random.normal(...)

```python
x_rv = pt.random.normal(mu, sigma, name='x')
```

### Step 4: Assign x_sum = pt.sum(...)

```python
x_sum = pt.sum(x_rv, axis=axis)
```

### Step 5: Assign x_sum_vv = pt.scalar(...)

```python
x_sum_vv = pt.scalar('x_sum')
```

### Step 6: Assign sum_logp = logp(...)

```python
sum_logp = logp(x_sum, x_sum_vv)
```

### Step 7: Assign ref_mu = pt.sum(...)

```python
ref_mu = pt.sum(mu, axis=axis)
```

### Step 8: Assign ref_sigma = pt.sqrt(...)

```python
ref_sigma = pt.sqrt(pt.sum(pt.square(sigma), axis=axis))
```

### Step 9: Assign ref_rv = pt.random.normal(...)

```python
ref_rv = pt.random.normal(ref_mu, ref_sigma, name='ref')
```

### Step 10: Assign ref_vv = pt.scalar(...)

```python
ref_vv = pt.scalar('ref_vv')
```

### Step 11: Assign ref_logp = logp(...)

```python
ref_logp = logp(ref_rv, ref_vv)
```

### Step 12: Assign test_val = 0.5

```python
test_val = 0.5
```

### Step 13: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(sum_logp.eval({x_sum_vv: test_val}), ref_logp.eval({ref_vv: test_val}))
```


## Complete Example

```python
# Setup
# Fixtures: axis

# Workflow
mu = pt.constant([[1.0, 2.0, 3.0], [0.5, 1.5, 2.5]])
sigma = pt.constant([[1.0, 2.0, 3.0], [1.5, 2.5, 3.5]])
x_rv = pt.random.normal(mu, sigma, name='x')
x_sum = pt.sum(x_rv, axis=axis)
x_sum_vv = pt.scalar('x_sum')
sum_logp = logp(x_sum, x_sum_vv)
ref_mu = pt.sum(mu, axis=axis)
ref_sigma = pt.sqrt(pt.sum(pt.square(sigma), axis=axis))
ref_rv = pt.random.normal(ref_mu, ref_sigma, name='ref')
ref_vv = pt.scalar('ref_vv')
ref_logp = logp(ref_rv, ref_vv)
test_val = 0.5
np.testing.assert_allclose(sum_logp.eval({x_sum_vv: test_val}), ref_logp.eval({ref_vv: test_val}))
```

## Next Steps


---

*Source: test_arithmetic.py:46 | Complexity: Advanced | Last updated: 2026-05-18*