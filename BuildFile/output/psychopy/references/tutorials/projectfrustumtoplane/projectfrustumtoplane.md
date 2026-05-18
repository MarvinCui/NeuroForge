# How To: Projectfrustumtoplane

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test the projection of the frustum to a plane.
    

## Prerequisites

**Required Modules:**
- `psychopy.tools.mathtools`
- `psychopy.tools.viewtools`
- `numpy`
- `pytest`


## Step-by-Step Guide

### Step 1: 'Test the projection of the frustum to a plane.\n    '

```python
'Test the projection of the frustum to a plane.\n    '
```

**Verification:**
```python
assert np.isclose(distance(topLeft, topRight), scrWidth) and np.isclose(distance(topLeft, bottomLeft), scrHeight)
```

### Step 2: Assign N = 1000

```python
N = 1000
```

### Step 3: Call np.random.seed()

```python
np.random.seed(12345)
```

### Step 4: Assign nearClip = 0.025

```python
nearClip = 0.025
```

### Step 5: Assign scrDims = np.random.uniform(...)

```python
scrDims = np.random.uniform(0.01, 10.0, (N, 2))
```

### Step 6: Assign viewDists = np.random.uniform(...)

```python
viewDists = np.random.uniform(nearClip, 10.0, (N,))
```

### Step 7: Assign eyeOffsets = np.random.uniform(...)

```python
eyeOffsets = np.random.uniform(-0.1, 0.1, (N,))
```

### Step 8: Assign scrWidth = value

```python
scrWidth = scrDims[i, 0]
```

### Step 9: Assign scrAspect = value

```python
scrAspect = scrDims[i, 0] / scrDims[i, 1]
```

### Step 10: Assign scrHeight = value

```python
scrHeight = scrWidth * (1.0 / scrAspect)
```

### Step 11: Assign viewDist = value

```python
viewDist = viewDists[i]
```

### Step 12: Assign farClip = viewDist

```python
farClip = viewDist
```

### Step 13: Assign frustum = computeFrustum(...)

```python
frustum = computeFrustum(scrWidth, scrAspect, viewDist, eyeOffset=eyeOffsets[i], nearClip=nearClip, farClip=farClip)
```

### Step 14: Assign frustum = value

```python
frustum = [v.item() for v in frustum]
```

### Step 15: Assign unknown = projectFrustumToPlane(...)

```python
topLeft, bottomLeft, _, topRight = projectFrustumToPlane(frustum, viewDist)
```

**Verification:**
```python
assert np.isclose(distance(topLeft, topRight), scrWidth) and np.isclose(distance(topLeft, bottomLeft), scrHeight)
```


## Complete Example

```python
# Workflow
'Test the projection of the frustum to a plane.\n    '
N = 1000
np.random.seed(12345)
nearClip = 0.025
scrDims = np.random.uniform(0.01, 10.0, (N, 2))
viewDists = np.random.uniform(nearClip, 10.0, (N,))
eyeOffsets = np.random.uniform(-0.1, 0.1, (N,))
for i in range(N):
    scrWidth = scrDims[i, 0]
    scrAspect = scrDims[i, 0] / scrDims[i, 1]
    scrHeight = scrWidth * (1.0 / scrAspect)
    viewDist = viewDists[i]
    farClip = viewDist
    frustum = computeFrustum(scrWidth, scrAspect, viewDist, eyeOffset=eyeOffsets[i], nearClip=nearClip, farClip=farClip)
    frustum = [v.item() for v in frustum]
    topLeft, bottomLeft, _, topRight = projectFrustumToPlane(frustum, viewDist)
    assert np.isclose(distance(topLeft, topRight), scrWidth) and np.isclose(distance(topLeft, bottomLeft), scrHeight)
```

## Next Steps


---

*Source: test_viewtools.py:73 | Complexity: Advanced | Last updated: 2026-05-18*