# How To: Bcast Rv Logp

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test that derived logp for broadcasted RV is correct

## Prerequisites

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


## Step-by-Step Guide

### Step 1: 'Test that derived logp for broadcasted RV is correct'

```python
'Test that derived logp for broadcasted RV is correct'
```

**Verification:**
```python
assert valid_logp.shape == ()
```

### Step 2: Assign x_rv = pt.random.normal(...)

```python
x_rv = pt.random.normal(name='x')
```

**Verification:**
```python
assert np.isclose(valid_logp, st.norm.logpdf(0))
```

### Step 3: Assign broadcasted_x_rv = pt.broadcast_to(...)

```python
broadcasted_x_rv = pt.broadcast_to(x_rv, (2,))
```

**Verification:**
```python
assert invalid_logp == -np.inf
```

### Step 4: Assign broadcasted_x_rv.name = 'broadcasted_x'

```python
broadcasted_x_rv.name = 'broadcasted_x'
```

### Step 5: Assign broadcasted_x_vv = broadcasted_x_rv.clone(...)

```python
broadcasted_x_vv = broadcasted_x_rv.clone()
```

### Step 6: Assign logp = conditional_logp(...)

```python
logp = conditional_logp({broadcasted_x_rv: broadcasted_x_vv})
```

### Step 7: Assign logp_combined = pt.add(...)

```python
logp_combined = pt.add(*logp.values())
```

### Step 8: Assign valid_logp = logp_combined.eval(...)

```python
valid_logp = logp_combined.eval({broadcasted_x_vv: [0, 0]})
```

**Verification:**
```python
assert valid_logp.shape == ()
```

### Step 9: Assign invalid_logp = logp_combined.eval(...)

```python
invalid_logp = logp_combined.eval({broadcasted_x_vv: [0, 1]})
```

**Verification:**
```python
assert invalid_logp == -np.inf
```


## Complete Example

```python
# Workflow
'Test that derived logp for broadcasted RV is correct'
x_rv = pt.random.normal(name='x')
broadcasted_x_rv = pt.broadcast_to(x_rv, (2,))
broadcasted_x_rv.name = 'broadcasted_x'
broadcasted_x_vv = broadcasted_x_rv.clone()
logp = conditional_logp({broadcasted_x_rv: broadcasted_x_vv})
logp_combined = pt.add(*logp.values())
valid_logp = logp_combined.eval({broadcasted_x_vv: [0, 0]})
assert valid_logp.shape == ()
assert np.isclose(valid_logp, st.norm.logpdf(0))
invalid_logp = logp_combined.eval({broadcasted_x_vv: [0, 1]})
assert invalid_logp == -np.inf
```

## Next Steps


---

*Source: test_tensor.py:52 | Complexity: Advanced | Last updated: 2026-05-18*