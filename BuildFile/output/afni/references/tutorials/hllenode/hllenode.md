# How To: Hllenode

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test HLLENode

## Prerequisites

**Required Modules:**
- `_tools`
- `test_ICANode`


## Step-by-Step Guide

### Step 1: Assign unknown = value

```python
n, k = (250, 4)
```

**Verification:**
```python
assert err.max() == 0
```

### Step 2: Assign unknown = _s_shape_1D(...)

```python
x, y, z, t = _s_shape_1D(n)
```

**Verification:**
```python
assert err.max() == 0
```

### Step 3: Assign data = value

```python
data = numx.asarray([x, y, z]).T
```

**Verification:**
```python
assert numx.all(res[idx, 1] - res[idx[0], 1] < 0.01), 'Projection should be aligned as original space'
```

### Step 4: Assign res = mdp.nodes.HLLENode(...)

```python
res = mdp.nodes.HLLENode(k, r=0.001, output_dim=1, svd=False)(data)
```

**Verification:**
```python
assert numx.all(res[idx, 0] - res[idx[0], 0] < 0.01), 'Projection should be aligned as original space'
```

### Step 5: Assign err = _compare_neighbors(...)

```python
err = _compare_neighbors(data, res, k)
```

**Verification:**
```python
assert err.max() == 0
```

### Step 6: Assign res = mdp.nodes.HLLENode(...)

```python
res = mdp.nodes.HLLENode(k, r=0.001, output_dim=1, svd=True)(data)
```

### Step 7: Assign err = _compare_neighbors(...)

```python
err = _compare_neighbors(data, res, k)
```

**Verification:**
```python
assert err.max() == 0
```

### Step 8: Assign unknown = value

```python
nt, ny = (40, 15)
```

### Step 9: Assign unknown = value

```python
n, k = (nt * ny, 8)
```

### Step 10: Assign unknown = _s_shape_2D(...)

```python
x, y, z, t = _s_shape_2D(nt, ny)
```

### Step 11: Assign data = value

```python
data = numx.asarray([x, y, z]).T
```

### Step 12: Assign res = mdp.nodes.HLLENode(...)

```python
res = mdp.nodes.HLLENode(k, r=0.001, output_dim=2, svd=False)(data)
```

### Step 13: Assign yval = value

```python
yval = y[::nt]
```

### Step 14: Assign tval = value

```python
tval = t[:ny]
```

### Step 15: Assign idx = value

```python
idx = numx.nonzero(y == yv)[0]
```

**Verification:**
```python
assert numx.all(res[idx, 1] - res[idx[0], 1] < 0.01), 'Projection should be aligned as original space'
```

### Step 16: Assign idx = value

```python
idx = numx.nonzero(t == tv)[0]
```

**Verification:**
```python
assert numx.all(res[idx, 0] - res[idx[0], 0] < 0.01), 'Projection should be aligned as original space'
```


## Complete Example

```python
# Workflow
n, k = (250, 4)
x, y, z, t = _s_shape_1D(n)
data = numx.asarray([x, y, z]).T
res = mdp.nodes.HLLENode(k, r=0.001, output_dim=1, svd=False)(data)
err = _compare_neighbors(data, res, k)
assert err.max() == 0
res = mdp.nodes.HLLENode(k, r=0.001, output_dim=1, svd=True)(data)
err = _compare_neighbors(data, res, k)
assert err.max() == 0
nt, ny = (40, 15)
n, k = (nt * ny, 8)
x, y, z, t = _s_shape_2D(nt, ny)
data = numx.asarray([x, y, z]).T
res = mdp.nodes.HLLENode(k, r=0.001, output_dim=2, svd=False)(data)
res[:, 0] /= res[:, 0].std()
res[:, 1] /= res[:, 1].std()
yval = y[::nt]
tval = t[:ny]
for yv in yval:
    idx = numx.nonzero(y == yv)[0]
    assert numx.all(res[idx, 1] - res[idx[0], 1] < 0.01), 'Projection should be aligned as original space'
for tv in tval:
    idx = numx.nonzero(t == tv)[0]
    assert numx.all(res[idx, 0] - res[idx[0], 0] < 0.01), 'Projection should be aligned as original space'
```

## Next Steps


---

*Source: test_contrib.py:161 | Complexity: Advanced | Last updated: 2026-05-18*