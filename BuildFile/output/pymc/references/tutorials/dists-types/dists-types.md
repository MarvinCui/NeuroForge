# How To: Dists Types

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test dists types

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

### Step 2: Assign innovation_dist = Normal.dist(...)

```python
innovation_dist = Normal.dist()
```

### Step 3: Assign init_dist = MvNormal.dist(...)

```python
init_dist = MvNormal.dist([0], [[1]])
```

### Step 4: Assign innovation_dist = Normal.dist(...)

```python
innovation_dist = Normal.dist(size=(1,))
```

### Step 5: Call RandomWalk.dist()

```python
RandomWalk.dist(init_dist=5, innovation_dist=innovation_dist, steps=5)
```

### Step 6: Call RandomWalk.dist()

```python
RandomWalk.dist(init_dist=init_dist, innovation_dist=5, steps=5)
```

### Step 7: Call RandomWalk.dist()

```python
RandomWalk.dist(init_dist=init_dist, innovation_dist=innovation_dist, steps=5)
```


## Complete Example

```python
# Workflow
init_dist = Normal.dist()
innovation_dist = Normal.dist()
with pytest.raises(TypeError, match='init_dist must be a distribution variable'):
    RandomWalk.dist(init_dist=5, innovation_dist=innovation_dist, steps=5)
with pytest.raises(TypeError, match='innovation_dist must be a distribution variable'):
    RandomWalk.dist(init_dist=init_dist, innovation_dist=5, steps=5)
init_dist = MvNormal.dist([0], [[1]])
innovation_dist = Normal.dist(size=(1,))
with pytest.raises(TypeError, match='init_dist and innovation_dist must have the same support dimensionality'):
    RandomWalk.dist(init_dist=init_dist, innovation_dist=innovation_dist, steps=5)
```

## Next Steps


---

*Source: test_timeseries.py:60 | Complexity: Intermediate | Last updated: 2026-05-18*