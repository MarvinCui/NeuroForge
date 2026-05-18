# How To: Min Logprob

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test whether the logprob for ```pt.mix``` produces the corrected
The fact that order statistics of i.i.d. uniform RVs ~ Beta is used here:
    U_1, \dots, U_n \stackrel{      ext{i.i.d.}}{\sim}      ext{Uniform}(0, 1) \Rightarrow U_{(k)} \sim     ext{Beta}(k, n + 1- k)
for all 1<=k<=n

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `re`
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `scipy.stats`
- `pymc`
- `pymc`
- `pymc.logprob`
- `pymc.testing`

**Setup Required:**
```python
# Fixtures: shape, value, axis
```

## Step-by-Step Guide

### Step 1: 'Test whether the logprob for ```pt.mix``` produces the corrected\n    The fact that order statistics of i.i.d. uniform RVs ~ Beta is used here:\n        U_1, \\dots, U_n \\stackrel{\text{i.i.d.}}{\\sim} \text{Uniform}(0, 1) \\Rightarrow U_{(k)} \\sim \text{Beta}(k, n + 1- k)\n    for all 1<=k<=n\n    '

```python
'Test whether the logprob for ```pt.mix``` produces the corrected\n    The fact that order statistics of i.i.d. uniform RVs ~ Beta is used here:\n        U_1, \\dots, U_n \\stackrel{\text{i.i.d.}}{\\sim} \text{Uniform}(0, 1) \\Rightarrow U_{(k)} \\sim \text{Beta}(k, n + 1- k)\n    for all 1<=k<=n\n    '
```

**Verification:**
```python
assert_no_rvs(x_min_logprob)
```

### Step 2: Assign x = pt.random.uniform(...)

```python
x = pt.random.uniform(0, 1, size=shape)
```

### Step 3: Assign x.name = 'x'

```python
x.name = 'x'
```

### Step 4: Assign x_min = pt.min(...)

```python
x_min = pt.min(x, axis=axis)
```

### Step 5: Assign x_min_value = pt.scalar(...)

```python
x_min_value = pt.scalar('x_min_value')
```

### Step 6: Assign x_min_logprob = logp(...)

```python
x_min_logprob = logp(x_min, x_min_value)
```

### Step 7: Call assert_no_rvs()

```python
assert_no_rvs(x_min_logprob)
```

### Step 8: Assign test_value = value

```python
test_value = value
```

### Step 9: Assign n = np.prod(...)

```python
n = np.prod(shape)
```

### Step 10: Assign beta_rv = pt.random.beta(...)

```python
beta_rv = pt.random.beta(1, n, name='beta')
```

### Step 11: Assign beta_vv = beta_rv.clone(...)

```python
beta_vv = beta_rv.clone()
```

### Step 12: Assign beta_rv_logprob = logp(...)

```python
beta_rv_logprob = logp(beta_rv, beta_vv)
```

### Step 13: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(beta_rv_logprob.eval({beta_vv: test_value}), x_min_logprob.eval({x_min_value: test_value}), rtol=1e-06)
```


## Complete Example

```python
# Setup
# Fixtures: shape, value, axis

# Workflow
'Test whether the logprob for ```pt.mix``` produces the corrected\n    The fact that order statistics of i.i.d. uniform RVs ~ Beta is used here:\n        U_1, \\dots, U_n \\stackrel{\text{i.i.d.}}{\\sim} \text{Uniform}(0, 1) \\Rightarrow U_{(k)} \\sim \text{Beta}(k, n + 1- k)\n    for all 1<=k<=n\n    '
x = pt.random.uniform(0, 1, size=shape)
x.name = 'x'
x_min = pt.min(x, axis=axis)
x_min_value = pt.scalar('x_min_value')
x_min_logprob = logp(x_min, x_min_value)
assert_no_rvs(x_min_logprob)
test_value = value
n = np.prod(shape)
beta_rv = pt.random.beta(1, n, name='beta')
beta_vv = beta_rv.clone()
beta_rv_logprob = logp(beta_rv, beta_vv)
np.testing.assert_allclose(beta_rv_logprob.eval({beta_vv: test_value}), x_min_logprob.eval({x_min_value: test_value}), rtol=1e-06)
```

## Next Steps


---

*Source: test_order.py:183 | Complexity: Advanced | Last updated: 2026-05-18*