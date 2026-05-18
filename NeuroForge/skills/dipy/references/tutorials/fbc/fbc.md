# How To: Fbc

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test the FBC measures on a set of fibers

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.core.sphere`
- `dipy.denoise.enhancement_kernel`
- `dipy.tracking.fbcmeasures`


## Step-by-Step Guide

### Step 1: 'Test the FBC measures on a set of fibers'

```python
'Test the FBC measures on a set of fibers'
```

### Step 2: Assign streamlines = value

```python
streamlines = []
```

### Step 3: Assign D33 = 1.0

```python
D33 = 1.0
```

### Step 4: Assign D44 = 0.04

```python
D44 = 0.04
```

### Step 5: Assign t = 1

```python
t = 1
```

### Step 6: Assign sphere = Sphere(...)

```python
sphere = Sphere(xyz=np.array([[0.82819078, 0.51050355, 0.23127074], [-0.10761926, -0.95554309, 0.27450957], [0.4101745, -0.07154038, 0.90919682], [-0.75573448, 0.64854889, 0.09082809], [-0.56874549, 0.01377562, 0.8223982]]))
```

### Step 7: Assign k = EnhancementKernel(...)

```python
k = EnhancementKernel(D33, D44, t, orientations=sphere, force_recompute=True)
```

### Step 8: Assign fbc = FBCMeasures(...)

```python
fbc = FBCMeasures(streamlines, k, verbose=True)
```

### Step 9: Assign unknown = fbc.get_points_rfbc_thresholded(...)

```python
fbc_sl_orig, clrs_orig, rfbc_orig = fbc.get_points_rfbc_thresholded(0, emphasis=0.01)
```

### Step 10: Call npt.assert_almost_equal()

```python
npt.assert_almost_equal(np.mean(rfbc_orig), 1.0500466494329224, decimal=4)
```

### Step 11: Assign fiber = np.zeros(...)

```python
fiber = np.zeros((10, 3))
```

### Step 12: Assign unknown = j

```python
fiber[j, 0] = j
```

### Step 13: Assign unknown = value

```python
fiber[j, 1] = i * 0.2
```

### Step 14: Assign unknown = 0

```python
fiber[j, 2] = 0
```

### Step 15: Call streamlines.append()

```python
streamlines.append(fiber)
```


## Complete Example

```python
# Workflow
'Test the FBC measures on a set of fibers'
streamlines = []
for i in range(2):
    fiber = np.zeros((10, 3))
    for j in range(10):
        fiber[j, 0] = j
        fiber[j, 1] = i * 0.2
        fiber[j, 2] = 0
        streamlines.append(fiber)
D33 = 1.0
D44 = 0.04
t = 1
sphere = Sphere(xyz=np.array([[0.82819078, 0.51050355, 0.23127074], [-0.10761926, -0.95554309, 0.27450957], [0.4101745, -0.07154038, 0.90919682], [-0.75573448, 0.64854889, 0.09082809], [-0.56874549, 0.01377562, 0.8223982]]))
k = EnhancementKernel(D33, D44, t, orientations=sphere, force_recompute=True)
fbc = FBCMeasures(streamlines, k, verbose=True)
fbc_sl_orig, clrs_orig, rfbc_orig = fbc.get_points_rfbc_thresholded(0, emphasis=0.01)
npt.assert_almost_equal(np.mean(rfbc_orig), 1.0500466494329224, decimal=4)
```

## Next Steps


---

*Source: test_fbc.py:9 | Complexity: Advanced | Last updated: 2026-05-18*