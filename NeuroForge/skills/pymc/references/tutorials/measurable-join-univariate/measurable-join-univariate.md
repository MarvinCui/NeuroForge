# How To: Measurable Join Univariate

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test measurable join univariate

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytensor`
- `pytest`
- `pytensor`
- `pytensor.graph`
- `pytensor.tensor.random.type`
- `scipy`
- `pymc.logprob.basic`
- `pymc.logprob.rewriting`
- `pymc.testing`

**Setup Required:**
```python
# Fixtures: size1, size2, axis, concatenate
```

## Step-by-Step Guide

### Step 1: Assign base1_rv = pt.random.normal(...)

```python
base1_rv = pt.random.normal(size=size1, name='base1')
```

**Verification:**
```python
assert_no_rvs(y_logp)
```

### Step 2: Assign base2_rv = pt.random.exponential(...)

```python
base2_rv = pt.random.exponential(size=size2, name='base2')
```

### Step 3: Assign y_rv.name = 'y'

```python
y_rv.name = 'y'
```

### Step 4: Assign base1_vv = base1_rv.clone(...)

```python
base1_vv = base1_rv.clone()
```

### Step 5: Assign base2_vv = base2_rv.clone(...)

```python
base2_vv = base2_rv.clone()
```

### Step 6: Assign y_vv = y_rv.clone(...)

```python
y_vv = y_rv.clone()
```

### Step 7: Assign base_logps = list(...)

```python
base_logps = list(conditional_logp({base1_rv: base1_vv, base2_rv: base2_vv}).values())
```

### Step 8: Assign y_logp = logp(...)

```python
y_logp = logp(y_rv, y_vv)
```

### Step 9: Call assert_no_rvs()

```python
assert_no_rvs(y_logp)
```

### Step 10: Assign base1_testval = base1_rv.eval(...)

```python
base1_testval = base1_rv.eval()
```

### Step 11: Assign base2_testval = base2_rv.eval(...)

```python
base2_testval = base2_rv.eval()
```

### Step 12: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(base_logps.eval({base1_vv: base1_testval, base2_vv: base2_testval}), y_logp.eval({y_vv: y_testval}))
```

### Step 13: Assign y_rv = pt.concatenate(...)

```python
y_rv = pt.concatenate((base1_rv, base2_rv), axis=axis)
```

### Step 14: Assign y_rv = pt.stack(...)

```python
y_rv = pt.stack((base1_rv, base2_rv), axis=axis)
```

### Step 15: Assign base_logps = pt.concatenate(...)

```python
base_logps = pt.concatenate(base_logps, axis=axis)
```

### Step 16: Assign base_logps = pt.stack(...)

```python
base_logps = pt.stack(base_logps, axis=axis)
```

### Step 17: Assign y_testval = np.concatenate(...)

```python
y_testval = np.concatenate((base1_testval, base2_testval), axis=axis)
```

### Step 18: Assign y_testval = np.stack(...)

```python
y_testval = np.stack((base1_testval, base2_testval), axis=axis)
```


## Complete Example

```python
# Setup
# Fixtures: size1, size2, axis, concatenate

# Workflow
base1_rv = pt.random.normal(size=size1, name='base1')
base2_rv = pt.random.exponential(size=size2, name='base2')
if concatenate:
    y_rv = pt.concatenate((base1_rv, base2_rv), axis=axis)
else:
    y_rv = pt.stack((base1_rv, base2_rv), axis=axis)
y_rv.name = 'y'
base1_vv = base1_rv.clone()
base2_vv = base2_rv.clone()
y_vv = y_rv.clone()
base_logps = list(conditional_logp({base1_rv: base1_vv, base2_rv: base2_vv}).values())
if concatenate:
    base_logps = pt.concatenate(base_logps, axis=axis)
else:
    base_logps = pt.stack(base_logps, axis=axis)
y_logp = logp(y_rv, y_vv)
assert_no_rvs(y_logp)
base1_testval = base1_rv.eval()
base2_testval = base2_rv.eval()
if concatenate:
    y_testval = np.concatenate((base1_testval, base2_testval), axis=axis)
else:
    y_testval = np.stack((base1_testval, base2_testval), axis=axis)
np.testing.assert_allclose(base_logps.eval({base1_vv: base1_testval, base2_vv: base2_testval}), y_logp.eval({y_vv: y_testval}))
```

## Next Steps


---

*Source: test_tensor.py:266 | Complexity: Advanced | Last updated: 2026-05-18*