# How To: Inferred Logp Mixture

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test inferred logp mixture

## Prerequisites

**Required Modules:**
- `warnings`
- `cloudpickle`
- `numpy`
- `pytensor`
- `pytest`
- `numpy`
- `pytensor`
- `pytensor`
- `pytensor.graph`
- `scipy`
- `pymc.distributions`
- `pymc.distributions.custom`
- `pymc.distributions.distribution`
- `pymc.distributions.shape_utils`
- `pymc.distributions.transforms`
- `pymc.exceptions`
- `pymc.logprob`
- `pymc.model`
- `pymc.pytensorf`
- `pymc.sampling`
- `pymc.step_methods`
- `pymc.testing`
- `numpy`


## Step-by-Step Guide

### Step 1: Assign mus = value

```python
mus = [3.5, -4.3]
```

### Step 2: Assign sds = value

```python
sds = [1.5, 2.3]
```

### Step 3: Assign w = value

```python
w = [0.3, 0.7]
```

### Step 4: Assign test_value = 0.1

```python
test_value = 0.1
```

### Step 5: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(m.compile_logp()({'mix': test_value}), logp(NormalMixture.dist(w=w, mu=mus, sigma=sds), test_value).eval())
```

### Step 6: Assign comp_dists = value

```python
comp_dists = [CustomDist.dist(mus[0], sds[0], dist=shifted_normal), CustomDist.dist(mus[1], sds[1], dist=shifted_normal)]
```

### Step 7: Call Mixture()

```python
Mixture('mix', w=w, comp_dists=comp_dists)
```


## Complete Example

```python
# Workflow
import numpy as np

def shifted_normal(mu, sigma, size):
    return mu + Normal.dist(0, sigma, shape=size)
mus = [3.5, -4.3]
sds = [1.5, 2.3]
w = [0.3, 0.7]
with Model() as m:
    comp_dists = [CustomDist.dist(mus[0], sds[0], dist=shifted_normal), CustomDist.dist(mus[1], sds[1], dist=shifted_normal)]
    Mixture('mix', w=w, comp_dists=comp_dists)
test_value = 0.1
np.testing.assert_allclose(m.compile_logp()({'mix': test_value}), logp(NormalMixture.dist(w=w, mu=mus, sigma=sds), test_value).eval())
```

## Next Steps


---

*Source: test_custom.py:589 | Complexity: Intermediate | Last updated: 2026-05-18*