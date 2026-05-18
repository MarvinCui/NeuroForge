# How To: Change Size Univariate

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test change size univariate

## Prerequisites

**Required Modules:**
- `numpy`
- `pytensor`
- `pytest`
- `scipy.stats`
- `pytensor.tensor.random.op`
- `pymc`
- `pymc`
- `pymc.distributions.continuous`
- `pymc.distributions.distribution`
- `pymc.distributions.multivariate`
- `pymc.distributions.shape_utils`
- `pymc.distributions.timeseries`
- `pymc.logprob.basic`
- `pymc.model`
- `pymc.pytensorf`
- `pymc.sampling.forward`
- `pymc.sampling.mcmc`
- `pymc.testing`


## Step-by-Step Guide

### Step 1: Assign init_dist = Normal.dist(...)

```python
init_dist = Normal.dist()
```

**Verification:**
```python
assert tuple(new_rw.shape.eval()) == (7, 100)
```

### Step 2: Assign innovation_dist = Normal.dist(...)

```python
innovation_dist = Normal.dist()
```

**Verification:**
```python
assert tuple(new_rw.shape.eval()) == (4, 3, 5, 100)
```

### Step 3: Assign rw = RandomWalk.dist(...)

```python
rw = RandomWalk.dist(init_dist=init_dist, innovation_dist=innovation_dist, shape=(5, 100))
```

### Step 4: Assign new_rw = change_dist_size(...)

```python
new_rw = change_dist_size(rw, new_size=(7,))
```

**Verification:**
```python
assert tuple(new_rw.shape.eval()) == (7, 100)
```

### Step 5: Assign new_rw = change_dist_size(...)

```python
new_rw = change_dist_size(rw, new_size=(4, 3), expand=True)
```

**Verification:**
```python
assert tuple(new_rw.shape.eval()) == (4, 3, 5, 100)
```


## Complete Example

```python
# Workflow
init_dist = Normal.dist()
innovation_dist = Normal.dist()
rw = RandomWalk.dist(init_dist=init_dist, innovation_dist=innovation_dist, shape=(5, 100))
new_rw = change_dist_size(rw, new_size=(7,))
assert tuple(new_rw.shape.eval()) == (7, 100)
new_rw = change_dist_size(rw, new_size=(4, 3), expand=True)
assert tuple(new_rw.shape.eval()) == (4, 3, 5, 100)
```

## Next Steps


---

*Source: test_timeseries.py:202 | Complexity: Intermediate | Last updated: 2026-05-18*