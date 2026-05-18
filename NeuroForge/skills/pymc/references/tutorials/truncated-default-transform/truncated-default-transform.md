# How To: Truncated Default Transform

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test truncated default transform

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

### Step 1: Assign base_dist = rejection_geometric(...)

```python
base_dist = rejection_geometric(1)
```

**Verification:**
```python
assert _default_transform(x.owner.op, x) is None
```

### Step 2: Assign x = Truncated.dist(...)

```python
x = Truncated.dist(base_dist, lower=None, upper=5)
```

**Verification:**
```python
assert isinstance(_default_transform(x.owner.op, x), IntervalTransform)
```

### Step 3: Assign base_dist = rejection_normal(...)

```python
base_dist = rejection_normal(0, 1)
```

### Step 4: Assign x = Truncated.dist(...)

```python
x = Truncated.dist(base_dist, lower=None, upper=5)
```

**Verification:**
```python
assert isinstance(_default_transform(x.owner.op, x), IntervalTransform)
```


## Complete Example

```python
# Workflow
base_dist = rejection_geometric(1)
x = Truncated.dist(base_dist, lower=None, upper=5)
assert _default_transform(x.owner.op, x) is None
base_dist = rejection_normal(0, 1)
x = Truncated.dist(base_dist, lower=None, upper=5)
assert isinstance(_default_transform(x.owner.op, x), IntervalTransform)
```

## Next Steps


---

*Source: test_truncated.py:378 | Complexity: Intermediate | Last updated: 2026-05-18*