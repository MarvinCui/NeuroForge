# How To: Affine Log Transform Rv

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test affine log transform rv

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

### Step 1: Assign unknown = pt.scalars(...)

```python
a, b = pt.scalars('a', 'b')
```

**Verification:**
```python
assert np.allclose(logp_fn(a_val, b_val, y_val), st.norm(a_val, b_val).logpdf(y_val))
```

### Step 2: Assign base_rv = pt.random.lognormal(...)

```python
base_rv = pt.random.lognormal(0, 1, name='base_rv', size=(1, 2))
```

### Step 3: Assign y_rv = value

```python
y_rv = a + pt.log(base_rv) * b
```

### Step 4: Assign y_rv.name = 'y'

```python
y_rv.name = 'y'
```

### Step 5: Assign y_vv = y_rv.clone(...)

```python
y_vv = y_rv.clone()
```

### Step 6: Assign logprob = logp(...)

```python
logprob = logp(y_rv, y_vv)
```

### Step 7: Assign logp_fn = pytensor.function(...)

```python
logp_fn = pytensor.function([a, b, y_vv], logprob)
```

### Step 8: Assign a_val = value

```python
a_val = -1.5
```

### Step 9: Assign b_val = 3.0

```python
b_val = 3.0
```

### Step 10: Assign y_val = value

```python
y_val = [[0.1, 0.1]]
```

**Verification:**
```python
assert np.allclose(logp_fn(a_val, b_val, y_val), st.norm(a_val, b_val).logpdf(y_val))
```


## Complete Example

```python
# Workflow
a, b = pt.scalars('a', 'b')
base_rv = pt.random.lognormal(0, 1, name='base_rv', size=(1, 2))
y_rv = a + pt.log(base_rv) * b
y_rv.name = 'y'
y_vv = y_rv.clone()
logprob = logp(y_rv, y_vv)
logp_fn = pytensor.function([a, b, y_vv], logprob)
a_val = -1.5
b_val = 3.0
y_val = [[0.1, 0.1]]
assert np.allclose(logp_fn(a_val, b_val, y_val), st.norm(a_val, b_val).logpdf(y_val))
```

## Next Steps


---

*Source: test_composite_logprob.py:200 | Complexity: Advanced | Last updated: 2026-05-18*