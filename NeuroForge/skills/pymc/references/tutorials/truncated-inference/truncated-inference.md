# How To: Truncated Inference

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test truncated inference

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

### Step 1: Assign lam_true = 3

```python
lam_true = 3
```

**Verification:**
```python
assert np.isclose(map['lam'], lam_true, atol=0.1)
```

### Step 2: Assign lower = 0

```python
lower = 0
```

### Step 3: Assign upper = 5

```python
upper = 5
```

### Step 4: Assign rng = np.random.default_rng(...)

```python
rng = np.random.default_rng(260)
```

### Step 5: Assign x = rng.exponential(...)

```python
x = rng.exponential(lam_true, size=5000)
```

### Step 6: Assign obs = value

```python
obs = x[np.where(~((x < lower) | (x > upper)))]
```

**Verification:**
```python
assert np.isclose(map['lam'], lam_true, atol=0.1)
```

### Step 7: Assign lam = Exponential(...)

```python
lam = Exponential('lam', lam=1 / 5)
```

### Step 8: Call Truncated()

```python
Truncated('x', dist=Exponential.dist(lam=1 / lam), lower=lower, upper=upper, observed=obs)
```

### Step 9: Assign map = find_MAP(...)

```python
map = find_MAP(progressbar=False)
```


## Complete Example

```python
# Workflow
lam_true = 3
lower = 0
upper = 5
rng = np.random.default_rng(260)
x = rng.exponential(lam_true, size=5000)
obs = x[np.where(~((x < lower) | (x > upper)))]
with Model() as m:
    lam = Exponential('lam', lam=1 / 5)
    Truncated('x', dist=Exponential.dist(lam=1 / lam), lower=lower, upper=upper, observed=obs)
    map = find_MAP(progressbar=False)
assert np.isclose(map['lam'], lam_true, atol=0.1)
```

## Next Steps


---

*Source: test_truncated.py:417 | Complexity: Advanced | Last updated: 2026-05-18*