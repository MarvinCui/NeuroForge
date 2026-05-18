# How To: Multigamma

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test multigamma

## Prerequisites

**Required Modules:**
- `numpy`
- `pytensor.tensor`
- `pytest`
- `scipy.special`
- `pytensor`
- `pytensor.tensor.random.basic`
- `scipy`
- `pymc`
- `pymc.distributions`
- `pymc.distributions.dist_math`
- `pymc.logprob.utils`
- `pymc.pytensorf`
- `tests.helpers`


## Step-by-Step Guide

### Step 1: Assign x = pt.vector(...)

```python
x = pt.vector('x', shape=(1,))
```

### Step 2: Assign p = pt.scalar(...)

```python
p = pt.scalar('p')
```

### Step 3: Assign xvals = value

```python
xvals = [np.array([v], dtype=config.floatX) for v in [0.1, 2, 5, 10, 50, 100]]
```

### Step 4: Assign multigammaln_ = function(...)

```python
multigammaln_ = function([x, p], multigammaln(x, p), mode='FAST_COMPILE')
```

### Step 5: Call check_vals()

```python
check_vals(multigammaln_, ref_multigammaln, x, p)
```


## Complete Example

```python
# Workflow
x = pt.vector('x', shape=(1,))
p = pt.scalar('p')
xvals = [np.array([v], dtype=config.floatX) for v in [0.1, 2, 5, 10, 50, 100]]
multigammaln_ = function([x, p], multigammaln(x, p), mode='FAST_COMPILE')

def ref_multigammaln(a, b):
    return np.array(scipy.special.multigammaln(a[0], b), config.floatX)
for p in [0, 1, 2, 3, 4, 100]:
    for x in xvals:
        if np.all(x > 0.5 * (p - 1)):
            check_vals(multigammaln_, ref_multigammaln, x, p)
```

## Next Steps


---

*Source: test_dist_math.py:159 | Complexity: Intermediate | Last updated: 2026-05-18*