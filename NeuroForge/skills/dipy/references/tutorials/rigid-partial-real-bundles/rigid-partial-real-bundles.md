# How To: Rigid Partial Real Bundles

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test rigid partial real bundles

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.align.bundlemin`
- `dipy.align.streamlinear`
- `dipy.core.geometry`
- `dipy.data`
- `dipy.io.streamline`
- `dipy.testing.decorators`
- `dipy.tracking.streamline`


## Step-by-Step Guide

### Step 1: Assign static = value

```python
static = fornix_streamlines()[:20]
```

**Verification:**
```python
assert_equal(overlap * 100 > 40, True)
```

### Step 2: Assign moving = value

```python
moving = fornix_streamlines()[20:40]
```

### Step 3: Assign unknown = center_streamlines(...)

```python
static_center, shift = center_streamlines(static)
```

### Step 4: Assign unknown = center_streamlines(...)

```python
moving_center, shift2 = center_streamlines(moving)
```

### Step 5: Call print()

```python
print(shift2)
```

### Step 6: Assign mat = compose_matrix(...)

```python
mat = compose_matrix(translate=np.array([0, 0, 0.0]), angles=np.deg2rad([40, 0, 0.0]))
```

### Step 7: Assign moved = transform_streamlines(...)

```python
moved = transform_streamlines(moving_center, mat)
```

### Step 8: Assign srr = StreamlineLinearRegistration(...)

```python
srr = StreamlineLinearRegistration()
```

### Step 9: Assign srm = srr.optimize(...)

```python
srm = srr.optimize(static_center, moved)
```

### Step 10: Call print()

```python
print(srm.fopt)
```

### Step 11: Call print()

```python
print(srm.iterations)
```

### Step 12: Call print()

```python
print(srm.funcs)
```

### Step 13: Assign moving_back = srm.transform(...)

```python
moving_back = srm.transform(moved)
```

### Step 14: Call print()

```python
print(srm.matrix)
```

### Step 15: Assign static_center = set_number_of_points(...)

```python
static_center = set_number_of_points(static_center, nb_points=100)
```

### Step 16: Assign moving_center = set_number_of_points(...)

```python
moving_center = set_number_of_points(moving_back, nb_points=100)
```

### Step 17: Assign vol = np.zeros(...)

```python
vol = np.zeros((100, 100, 100))
```

### Step 18: Assign spts = np.concatenate(...)

```python
spts = np.concatenate(static_center, axis=0)
```

### Step 19: Assign spts = value

```python
spts = np.round(spts).astype(int) + np.array([50, 50, 50])
```

### Step 20: Assign mpts = np.concatenate(...)

```python
mpts = np.concatenate(moving_center, axis=0)
```

### Step 21: Assign mpts = value

```python
mpts = np.round(mpts).astype(int) + np.array([50, 50, 50])
```

### Step 22: Assign vol2 = np.zeros(...)

```python
vol2 = np.zeros((100, 100, 100))
```

### Step 23: Assign overlap = value

```python
overlap = np.sum(np.logical_and(vol, vol2)) / float(np.sum(vol2))
```

### Step 24: Call assert_equal()

```python
assert_equal(overlap * 100 > 40, True)
```

### Step 25: Assign unknown = index

```python
i, j, k = index
```

### Step 26: Assign unknown = 1

```python
vol[i, j, k] = 1
```

### Step 27: Assign unknown = index

```python
i, j, k = index
```

### Step 28: Assign unknown = 1

```python
vol2[i, j, k] = 1
```


## Complete Example

```python
# Workflow
static = fornix_streamlines()[:20]
moving = fornix_streamlines()[20:40]
static_center, shift = center_streamlines(static)
moving_center, shift2 = center_streamlines(moving)
print(shift2)
mat = compose_matrix(translate=np.array([0, 0, 0.0]), angles=np.deg2rad([40, 0, 0.0]))
moved = transform_streamlines(moving_center, mat)
srr = StreamlineLinearRegistration()
srm = srr.optimize(static_center, moved)
print(srm.fopt)
print(srm.iterations)
print(srm.funcs)
moving_back = srm.transform(moved)
print(srm.matrix)
static_center = set_number_of_points(static_center, nb_points=100)
moving_center = set_number_of_points(moving_back, nb_points=100)
vol = np.zeros((100, 100, 100))
spts = np.concatenate(static_center, axis=0)
spts = np.round(spts).astype(int) + np.array([50, 50, 50])
mpts = np.concatenate(moving_center, axis=0)
mpts = np.round(mpts).astype(int) + np.array([50, 50, 50])
for index in spts:
    i, j, k = index
    vol[i, j, k] = 1
vol2 = np.zeros((100, 100, 100))
for index in mpts:
    i, j, k = index
    vol2[i, j, k] = 1
overlap = np.sum(np.logical_and(vol, vol2)) / float(np.sum(vol2))
assert_equal(overlap * 100 > 40, True)
```

## Next Steps


---

*Source: test_streamlinear.py:119 | Complexity: Advanced | Last updated: 2026-05-18*