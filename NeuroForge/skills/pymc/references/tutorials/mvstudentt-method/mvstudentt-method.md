# How To: Mvstudentt Method

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test mvstudentt method

## Prerequisites

**Required Modules:**
- `functools`
- `warnings`
- `numpy`
- `numpy.random`
- `numpy.testing`
- `pytensor`
- `pytest`
- `scipy.special`
- `scipy.stats`
- `pytensor`
- `pytensor.compile.mode`
- `pytensor.tensor`
- `pytensor.tensor.blockwise`
- `pytensor.tensor.linalg.decomposition.cholesky`
- `pytensor.tensor.linalg.inverse`
- `pytensor.tensor.random.basic`
- `pytensor.tensor.random.utils`
- `pymc`
- `pymc`
- `pymc.distributions.multivariate`
- `pymc.distributions.shape_utils`
- `pymc.distributions.transforms`
- `pymc.logprob.basic`
- `pymc.logprob.utils`
- `pymc.math`
- `pymc.pytensorf`
- `pymc.sampling.forward`
- `pymc.testing`


## Step-by-Step Guide

### Step 1: Assign x = pm.MvStudentT.dist(...)

```python
x = pm.MvStudentT.dist(nu=4, scale=np.eye(3), method='svd')
```

**Verification:**
```python
assert x.type.shape == (3,)
```

### Step 2: Assign resized_x = change_dist_size(...)

```python
resized_x = change_dist_size(x, (2,))
```

**Verification:**
```python
assert all_svd_method(x.owner.op.fgraph)
```

### Step 3: Assign found_one = False

```python
found_one = False
```

**Verification:**
```python
assert resized_x.type.shape == (2, 3)
```

### Step 4: Assign found_one = True

```python
found_one = True
```

**Verification:**
```python
assert all_svd_method(resized_x.owner.op.fgraph)
```


## Complete Example

```python
# Workflow
def all_svd_method(fgraph):
    found_one = False
    for node in fgraph.toposort():
        if isinstance(node.op, pm.MvNormal):
            found_one = True
            if not node.op.method == 'svd':
                return False
    return found_one
x = pm.MvStudentT.dist(nu=4, scale=np.eye(3), method='svd')
assert x.type.shape == (3,)
assert all_svd_method(x.owner.op.fgraph)
resized_x = change_dist_size(x, (2,))
assert resized_x.type.shape == (2, 3)
assert all_svd_method(resized_x.owner.op.fgraph)
```

## Next Steps


---

*Source: test_multivariate.py:2595 | Complexity: Intermediate | Last updated: 2026-05-18*