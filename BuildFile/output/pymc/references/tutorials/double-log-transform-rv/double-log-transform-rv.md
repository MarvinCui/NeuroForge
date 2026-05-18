# How To: Double Log Transform Rv

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test double log transform rv

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

### Step 1: Assign base_rv = pt.random.normal(...)

```python
base_rv = pt.random.normal(0, 1)
```

### Step 2: Assign y_rv = pt.log(...)

```python
y_rv = pt.log(pt.log(base_rv))
```

### Step 3: Assign y_rv.name = 'y'

```python
y_rv.name = 'y'
```

### Step 4: Assign y_vv = y_rv.clone(...)

```python
y_vv = y_rv.clone()
```

### Step 5: Assign logprob = logp(...)

```python
logprob = logp(y_rv, y_vv)
```

### Step 6: Assign logp_fn = pytensor.function(...)

```python
logp_fn = pytensor.function([y_vv], logprob)
```

### Step 7: Assign log_log_y_val = np.asarray(...)

```python
log_log_y_val = np.asarray(0.5)
```

### Step 8: Assign log_y_val = np.exp(...)

```python
log_y_val = np.exp(log_log_y_val)
```

### Step 9: Assign y_val = np.exp(...)

```python
y_val = np.exp(log_y_val)
```

### Step 10: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(logp_fn(log_log_y_val), st.norm().logpdf(y_val) + log_y_val + log_log_y_val)
```


## Complete Example

```python
# Workflow
base_rv = pt.random.normal(0, 1)
y_rv = pt.log(pt.log(base_rv))
y_rv.name = 'y'
y_vv = y_rv.clone()
logprob = logp(y_rv, y_vv)
logp_fn = pytensor.function([y_vv], logprob)
log_log_y_val = np.asarray(0.5)
log_y_val = np.exp(log_log_y_val)
y_val = np.exp(log_y_val)
np.testing.assert_allclose(logp_fn(log_log_y_val), st.norm().logpdf(y_val) + log_y_val + log_log_y_val)
```

## Next Steps


---

*Source: test_composite_logprob.py:159 | Complexity: Advanced | Last updated: 2026-05-18*