# How To: Adjacency Calc

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test adjacency_calc function, which calculates indices of adjacent voxels

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.utils.volume`


## Step-by-Step Guide

### Step 1: '\n    Test adjacency_calc function, which calculates indices of adjacent voxels\n    '

```python
'\n    Test adjacency_calc function, which calculates indices of adjacent voxels\n    '
```

### Step 2: Assign cutoff = 1.99

```python
cutoff = 1.99
```

### Step 3: Assign mask = None

```python
mask = None
```

### Step 4: Assign adj = adjacency_calc(...)

```python
adj = adjacency_calc(img_shape, mask=mask, cutoff=cutoff)
```

### Step 5: Call unknown.sort()

```python
adj[0].sort()
```

### Step 6: Assign mask = np.zeros(...)

```python
mask = np.zeros(img_shape, dtype=int)
```

### Step 7: Assign adj = adjacency_calc(...)

```python
adj = adjacency_calc(img_shape, mask=mask, cutoff=cutoff)
```

### Step 8: Call npt.assert_equal()

```python
npt.assert_equal(len(adj), mask.sum())
```

### Step 9: Call npt.assert_equal()

```python
npt.assert_equal(adj[0], [0, 1, 50, 51])
```

### Step 10: Call npt.assert_equal()

```python
npt.assert_equal(adj[0], [0, 1, 5, 6, 250, 251, 255, 256])
```

### Step 11: Assign unknown = 1

```python
mask[10:40, 20:30] = 1
```

### Step 12: Assign unknown = 1

```python
mask[10:40, 20:30, :] = 1
```

### Step 13: Call npt.assert_equal()

```python
npt.assert_equal(adj[0], [0, 1, 10, 11])
```

### Step 14: Call npt.assert_equal()

```python
npt.assert_equal(adj[0], [0, 1, 5, 6, 50, 51, 55, 56])
```


## Complete Example

```python
# Workflow
'\n    Test adjacency_calc function, which calculates indices of adjacent voxels\n    '
cutoff = 1.99
for img_shape in [(50, 50), (50, 50, 5)]:
    mask = None
    adj = adjacency_calc(img_shape, mask=mask, cutoff=cutoff)
    adj[0].sort()
    if len(img_shape) == 2:
        npt.assert_equal(adj[0], [0, 1, 50, 51])
    if len(img_shape) == 3:
        npt.assert_equal(adj[0], [0, 1, 5, 6, 250, 251, 255, 256])
    mask = np.zeros(img_shape, dtype=int)
    if len(img_shape) == 2:
        mask[10:40, 20:30] = 1
    if len(img_shape) == 3:
        mask[10:40, 20:30, :] = 1
    adj = adjacency_calc(img_shape, mask=mask, cutoff=cutoff)
    if len(img_shape) == 2:
        npt.assert_equal(adj[0], [0, 1, 10, 11])
    if len(img_shape) == 3:
        npt.assert_equal(adj[0], [0, 1, 5, 6, 50, 51, 55, 56])
    npt.assert_equal(len(adj), mask.sum())
```

## Next Steps


---

*Source: test_volume.py:9 | Complexity: Advanced | Last updated: 2026-05-18*