# How To: Truncated Transform Logp

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test truncated transform logp

## Prerequisites

**Required Modules:**
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `scipy`
- `pytensor.scalar`
- `pytensor.scan.op`
- `pytensor.tensor.random.basic`
- `pytensor.tensor.random.type`
- `pymc`
- `pymc.distributions`
- `pymc.distributions.shape_utils`
- `pymc.distributions.transforms`
- `pymc.distributions.truncated`
- `pymc.exceptions`
- `pymc.logprob.abstract`
- `pymc.logprob.basic`
- `pymc.logprob.transforms`
- `pymc.logprob.utils`
- `pymc.pytensorf`
- `pymc.testing`


## Step-by-Step Guide

### Step 1: Assign base_dist = rejection_normal(...)

```python
base_dist = rejection_normal(0, 1)
```

**Verification:**
```python
assert logp_eval[0] == -np.inf
```

### Step 2: Assign x = Truncated(...)

```python
x = Truncated('x', base_dist, lower=0, upper=None, default_transform=None)
```

**Verification:**
```python
assert np.isfinite(logp_eval[1])
```

### Step 3: Assign y = Truncated(...)

```python
y = Truncated('y', base_dist, lower=0, upper=None)
```

### Step 4: Assign logp_eval = m.compile_logp(...)

```python
logp_eval = m.compile_logp(sum=False)({'x': -1, 'y_interval__': -1})
```


## Complete Example

```python
# Workflow
with Model() as m:
    base_dist = rejection_normal(0, 1)
    x = Truncated('x', base_dist, lower=0, upper=None, default_transform=None)
    y = Truncated('y', base_dist, lower=0, upper=None)
    logp_eval = m.compile_logp(sum=False)({'x': -1, 'y_interval__': -1})
assert logp_eval[0] == -np.inf
assert np.isfinite(logp_eval[1])
```

## Next Steps


---

*Source: test_truncated.py:388 | Complexity: Intermediate | Last updated: 2026-05-18*