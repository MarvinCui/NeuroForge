# How To: Potentially Measurable Operand

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test potentially measurable operand

## Prerequisites

**Required Modules:**
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `scipy.stats`
- `pytensor`
- `pymc`
- `pymc.logprob`
- `pymc.testing`


## Step-by-Step Guide

### Step 1: Assign x_rv = pt.random.normal(...)

```python
x_rv = pt.random.normal(2)
```

**Verification:**
```python
assert_no_rvs(logprob)
```

### Step 2: Assign z_rv = pt.random.normal(...)

```python
z_rv = pt.random.normal(x_rv)
```

### Step 3: Assign y_rv = pt.lt(...)

```python
y_rv = pt.lt(x_rv, z_rv)
```

### Step 4: Assign y_vv = y_rv.clone(...)

```python
y_vv = y_rv.clone()
```

### Step 5: Assign z_vv = z_rv.clone(...)

```python
z_vv = z_rv.clone()
```

### Step 6: Assign logprob = value

```python
logprob = conditional_logp({z_rv: z_vv, y_rv: y_vv})[y_vv]
```

### Step 7: Call assert_no_rvs()

```python
assert_no_rvs(logprob)
```

### Step 8: Assign fn = function(...)

```python
fn = function([z_vv, y_vv], logprob)
```

### Step 9: Assign z_vv_test = 0.5

```python
z_vv_test = 0.5
```

### Step 10: Assign y_vv_test = True

```python
y_vv_test = True
```

### Step 11: Call np.testing.assert_array_almost_equal()

```python
np.testing.assert_array_almost_equal(fn(z_vv_test, y_vv_test), st.norm(2, 1).logcdf(z_vv_test))
```

### Step 12: Call logp.eval()

```python
logp(y_rv, y_vv).eval({y_vv: y_vv_test})
```


## Complete Example

```python
# Workflow
x_rv = pt.random.normal(2)
z_rv = pt.random.normal(x_rv)
y_rv = pt.lt(x_rv, z_rv)
y_vv = y_rv.clone()
z_vv = z_rv.clone()
logprob = conditional_logp({z_rv: z_vv, y_rv: y_vv})[y_vv]
assert_no_rvs(logprob)
fn = function([z_vv, y_vv], logprob)
z_vv_test = 0.5
y_vv_test = True
np.testing.assert_array_almost_equal(fn(z_vv_test, y_vv_test), st.norm(2, 1).logcdf(z_vv_test))
with pytest.raises(NotImplementedError, match='Logprob method not implemented'):
    logp(y_rv, y_vv).eval({y_vv: y_vv_test})
```

## Next Steps


---

*Source: test_binary.py:126 | Complexity: Advanced | Last updated: 2026-05-18*