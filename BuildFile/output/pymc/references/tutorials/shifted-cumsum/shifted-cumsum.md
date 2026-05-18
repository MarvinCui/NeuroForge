# How To: Shifted Cumsum

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test shifted cumsum

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

### Step 1: Assign x = pt.random.normal(...)

```python
x = pt.random.normal(size=(5,), name='x')
```

**Verification:**
```python
assert np.isclose(logprob.eval({y_vv: np.arange(5) + 1 + 5}).sum(), st.norm.logpdf(1) * 5)
```

### Step 2: Assign y = value

```python
y = 5 + pt.cumsum(x)
```

### Step 3: Assign y.name = 'y'

```python
y.name = 'y'
```

### Step 4: Assign y_vv = y.clone(...)

```python
y_vv = y.clone()
```

### Step 5: Assign logprob = logp(...)

```python
logprob = logp(y, y_vv)
```

**Verification:**
```python
assert np.isclose(logprob.eval({y_vv: np.arange(5) + 1 + 5}).sum(), st.norm.logpdf(1) * 5)
```


## Complete Example

```python
# Workflow
x = pt.random.normal(size=(5,), name='x')
y = 5 + pt.cumsum(x)
y.name = 'y'
y_vv = y.clone()
logprob = logp(y, y_vv)
assert np.isclose(logprob.eval({y_vv: np.arange(5) + 1 + 5}).sum(), st.norm.logpdf(1) * 5)
```

## Next Steps


---

*Source: test_composite_logprob.py:146 | Complexity: Intermediate | Last updated: 2026-05-18*