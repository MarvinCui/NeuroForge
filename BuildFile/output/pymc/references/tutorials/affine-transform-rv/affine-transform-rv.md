# How To: Affine Transform Rv

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test affine transform rv

## Prerequisites

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


## Step-by-Step Guide

### Step 1: Assign loc = pt.scalar(...)

```python
loc = pt.scalar('loc')
```

**Verification:**
```python
assert_no_rvs(logprob)
```

### Step 2: Assign scale = pt.vector(...)

```python
scale = pt.vector('scale')
```

### Step 3: Assign rv_size = 3

```python
rv_size = 3
```

### Step 4: Assign y_rv = value

```python
y_rv = loc + pt.random.normal(0, 1, size=rv_size, name='base_rv') * scale
```

### Step 5: Assign y_rv.name = 'y'

```python
y_rv.name = 'y'
```

### Step 6: Assign y_vv = y_rv.clone(...)

```python
y_vv = y_rv.clone()
```

### Step 7: Assign logprob = logp(...)

```python
logprob = logp(y_rv, y_vv)
```

### Step 8: Call assert_no_rvs()

```python
assert_no_rvs(logprob)
```

### Step 9: Assign logp_fn = pytensor.function(...)

```python
logp_fn = pytensor.function([loc, scale, y_vv], logprob)
```

### Step 10: Assign loc_test_val = 4.0

```python
loc_test_val = 4.0
```

### Step 11: Assign scale_test_val = np.full(...)

```python
scale_test_val = np.full(rv_size, 0.5)
```

### Step 12: Assign y_test_val = np.full(...)

```python
y_test_val = np.full(rv_size, 1.0)
```

### Step 13: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(logp_fn(loc_test_val, scale_test_val, y_test_val), st.norm(loc_test_val, scale_test_val).logpdf(y_test_val))
```


## Complete Example

```python
# Workflow
loc = pt.scalar('loc')
scale = pt.vector('scale')
rv_size = 3
y_rv = loc + pt.random.normal(0, 1, size=rv_size, name='base_rv') * scale
y_rv.name = 'y'
y_vv = y_rv.clone()
logprob = logp(y_rv, y_vv)
assert_no_rvs(logprob)
logp_fn = pytensor.function([loc, scale, y_vv], logprob)
loc_test_val = 4.0
scale_test_val = np.full(rv_size, 0.5)
y_test_val = np.full(rv_size, 1.0)
np.testing.assert_allclose(logp_fn(loc_test_val, scale_test_val, y_test_val), st.norm(loc_test_val, scale_test_val).logpdf(y_test_val))
```

## Next Steps


---

*Source: test_composite_logprob.py:177 | Complexity: Advanced | Last updated: 2026-05-18*