# How To: Frustumtoprojectionmatrix

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Ensure the `computeFrustum` + `perspectiveProjectionMatrix` and
`generalizedPerspectiveProjection` give similar results, therefore testing
them both at the same time.

## Prerequisites

**Required Modules:**
- `psychopy.tools.mathtools`
- `psychopy.tools.viewtools`
- `numpy`
- `pytest`


## Step-by-Step Guide

### Step 1: 'Ensure the `computeFrustum` + `perspectiveProjectionMatrix` and\n    `generalizedPerspectiveProjection` give similar results, therefore testing\n    them both at the same time.\n\n    '

```python
'Ensure the `computeFrustum` + `perspectiveProjectionMatrix` and\n    `generalizedPerspectiveProjection` give similar results, therefore testing\n    them both at the same time.\n\n    '
```

**Verification:**
```python
assert np.allclose(P, GP)
```

### Step 2: Assign N = 1000

```python
N = 1000
```

### Step 3: Call np.random.seed()

```python
np.random.seed(12345)
```

### Step 4: Assign scrDims = np.random.uniform(...)

```python
scrDims = np.random.uniform(0.01, 10.0, (N, 2))
```

### Step 5: Assign viewDists = np.random.uniform(...)

```python
viewDists = np.random.uniform(0.025, 10.0, (N,))
```

### Step 6: Assign eyeOffsets = np.random.uniform(...)

```python
eyeOffsets = np.random.uniform(-0.1, 0.1, (N,))
```

### Step 7: Assign scrWidth = value

```python
scrWidth = scrDims[i, 0]
```

### Step 8: Assign scrAspect = value

```python
scrAspect = scrDims[i, 0] / scrDims[i, 1]
```

### Step 9: Assign viewDist = value

```python
viewDist = viewDists[i]
```

### Step 10: Assign nearClip = np.random.uniform(...)

```python
nearClip = np.random.uniform(0.001, viewDist, (1,))
```

### Step 11: Assign fcMin = value

```python
fcMin = viewDist + nearClip
```

### Step 12: Assign farClip = np.random.uniform(...)

```python
farClip = np.random.uniform(fcMin, 1000.0, (1,))
```

### Step 13: Assign frustum = computeFrustum(...)

```python
frustum = computeFrustum(scrWidth, scrAspect, viewDist, eyeOffset=eyeOffsets[i], nearClip=nearClip, farClip=farClip)
```

### Step 14: Assign frustum = value

```python
frustum = [v.item() for v in frustum]
```

### Step 15: Assign P = perspectiveProjectionMatrix(...)

```python
P = perspectiveProjectionMatrix(*frustum)
```

### Step 16: Assign x = value

```python
x = scrWidth / 2.0
```

### Step 17: Assign y = value

```python
y = scrDims[i, 1] / 2.0
```

### Step 18: Assign z = value

```python
z = -viewDist
```

### Step 19: Assign posBottomLeft = value

```python
posBottomLeft = [-x, -y, z]
```

### Step 20: Assign posBottomRight = value

```python
posBottomRight = [x, -y, z]
```

### Step 21: Assign posTopLeft = value

```python
posTopLeft = [-x, y, z]
```

### Step 22: Assign posEye = value

```python
posEye = [eyeOffsets[i], 0.0, 0.0]
```

### Step 23: Assign unknown = generalizedPerspectiveProjection(...)

```python
GP, _ = generalizedPerspectiveProjection(posBottomLeft, posBottomRight, posTopLeft, posEye, nearClip=nearClip, farClip=farClip)
```

**Verification:**
```python
assert np.allclose(P, GP)
```


## Complete Example

```python
# Workflow
'Ensure the `computeFrustum` + `perspectiveProjectionMatrix` and\n    `generalizedPerspectiveProjection` give similar results, therefore testing\n    them both at the same time.\n\n    '
N = 1000
np.random.seed(12345)
scrDims = np.random.uniform(0.01, 10.0, (N, 2))
viewDists = np.random.uniform(0.025, 10.0, (N,))
eyeOffsets = np.random.uniform(-0.1, 0.1, (N,))
for i in range(N):
    scrWidth = scrDims[i, 0]
    scrAspect = scrDims[i, 0] / scrDims[i, 1]
    viewDist = viewDists[i]
    nearClip = np.random.uniform(0.001, viewDist, (1,))
    fcMin = viewDist + nearClip
    farClip = np.random.uniform(fcMin, 1000.0, (1,))
    frustum = computeFrustum(scrWidth, scrAspect, viewDist, eyeOffset=eyeOffsets[i], nearClip=nearClip, farClip=farClip)
    frustum = [v.item() for v in frustum]
    P = perspectiveProjectionMatrix(*frustum)
    x = scrWidth / 2.0
    y = scrDims[i, 1] / 2.0
    z = -viewDist
    posBottomLeft = [-x, -y, z]
    posBottomRight = [x, -y, z]
    posTopLeft = [-x, y, z]
    posEye = [eyeOffsets[i], 0.0, 0.0]
    GP, _ = generalizedPerspectiveProjection(posBottomLeft, posBottomRight, posTopLeft, posEye, nearClip=nearClip, farClip=farClip)
    assert np.allclose(P, GP)
```

## Next Steps


---

*Source: test_viewtools.py:110 | Complexity: Advanced | Last updated: 2026-05-18*