# How To: Affine Join Interdependent

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test affine join interdependent

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `scipy.stats`
- `pymc`
- `pymc.logprob.abstract`
- `pymc.logprob.basic`
- `pymc.logprob.rewriting`
- `pymc.testing`

**Setup Required:**
```python
# Fixtures: reverse
```

## Step-by-Step Guide

### Step 1: Assign x = pt.random.normal(...)

```python
x = pt.random.normal(name='x')
```

**Verification:**
```python
assert_no_rvs(logp_combined)
```

### Step 2: Assign y_rvs = value

```python
y_rvs = []
```

### Step 3: Assign prev_rv = x

```python
prev_rv = x
```

### Step 4: Assign ys = pt.concatenate(...)

```python
ys = pt.concatenate(y_rvs, axis=0)
```

### Step 5: Assign ys.name = 'ys'

```python
ys.name = 'ys'
```

### Step 6: Assign x_vv = x.clone(...)

```python
x_vv = x.clone()
```

### Step 7: Assign ys_vv = ys.clone(...)

```python
ys_vv = ys.clone()
```

### Step 8: Assign logp = conditional_logp(...)

```python
logp = conditional_logp({x: x_vv, ys: ys_vv})
```

### Step 9: Assign logp_combined = pt.sum(...)

```python
logp_combined = pt.sum([pt.sum(factor) for factor in logp.values()])
```

### Step 10: Call assert_no_rvs()

```python
assert_no_rvs(logp_combined)
```

### Step 11: Assign y0_vv = unknown.clone(...)

```python
y0_vv = y_rvs[0].clone()
```

### Step 12: Assign y1_vv = unknown.clone(...)

```python
y1_vv = y_rvs[1].clone()
```

### Step 13: Assign y2_vv = unknown.clone(...)

```python
y2_vv = y_rvs[2].clone()
```

### Step 14: Assign ref_logp = conditional_logp(...)

```python
ref_logp = conditional_logp({x: x_vv, y_rvs[0]: y0_vv, y_rvs[1]: y1_vv, y_rvs[2]: y2_vv})
```

### Step 15: Assign ref_logp_combined = pt.sum(...)

```python
ref_logp_combined = pt.sum([pt.sum(factor) for factor in ref_logp.values()])
```

### Step 16: Assign rng = np.random.default_rng(...)

```python
rng = np.random.default_rng()
```

### Step 17: Assign unknown = draw(...)

```python
x_vv_test, ys_vv_test = draw([x, ys], random_seed=rng)
```

### Step 18: Assign ys_vv_test = rng.normal(...)

```python
ys_vv_test = rng.normal(size=(3, 2))
```

### Step 19: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(logp_combined.eval({x_vv: x_vv_test, ys_vv: ys_vv_test}), ref_logp_combined.eval({x_vv: x_vv_test, y0_vv: ys_vv_test[0:1], y1_vv: ys_vv_test[1:2], y2_vv: ys_vv_test[2:3]}))
```

### Step 20: Assign next_rv = pt.exp(...)

```python
next_rv = pt.exp(prev_rv + pt.random.beta(3, 1, name=f'y{i}', size=(1, 2)))
```

### Step 21: Call y_rvs.append()

```python
y_rvs.append(next_rv)
```

### Step 22: Assign prev_rv = next_rv

```python
prev_rv = next_rv
```

### Step 23: Assign y_rvs = value

```python
y_rvs = y_rvs[::-1]
```


## Complete Example

```python
# Setup
# Fixtures: reverse

# Workflow
x = pt.random.normal(name='x')
y_rvs = []
prev_rv = x
for i in range(3):
    next_rv = pt.exp(prev_rv + pt.random.beta(3, 1, name=f'y{i}', size=(1, 2)))
    y_rvs.append(next_rv)
    prev_rv = next_rv
if reverse:
    y_rvs = y_rvs[::-1]
ys = pt.concatenate(y_rvs, axis=0)
ys.name = 'ys'
x_vv = x.clone()
ys_vv = ys.clone()
logp = conditional_logp({x: x_vv, ys: ys_vv})
logp_combined = pt.sum([pt.sum(factor) for factor in logp.values()])
assert_no_rvs(logp_combined)
y0_vv = y_rvs[0].clone()
y1_vv = y_rvs[1].clone()
y2_vv = y_rvs[2].clone()
ref_logp = conditional_logp({x: x_vv, y_rvs[0]: y0_vv, y_rvs[1]: y1_vv, y_rvs[2]: y2_vv})
ref_logp_combined = pt.sum([pt.sum(factor) for factor in ref_logp.values()])
rng = np.random.default_rng()
x_vv_test, ys_vv_test = draw([x, ys], random_seed=rng)
ys_vv_test = rng.normal(size=(3, 2))
np.testing.assert_allclose(logp_combined.eval({x_vv: x_vv_test, ys_vv: ys_vv_test}), ref_logp_combined.eval({x_vv: x_vv_test, y0_vv: ys_vv_test[0:1], y1_vv: ys_vv_test[1:2], y2_vv: ys_vv_test[2:3]}))
```

## Next Steps


---

*Source: test_composite_logprob.py:222 | Complexity: Advanced | Last updated: 2026-05-18*