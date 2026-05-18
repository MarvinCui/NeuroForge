# How To: Nearestneighborinterpolator

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test NearestNeighborInterpolator

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `scipy.ndimage`
- `dipy.align`
- `dipy.core.interpolation`
- `dipy.core.subdivide_octahedron`
- `dipy.testing.decorators`


## Step-by-Step Guide

### Step 1: Assign unknown = value

```python
ell, m, n, o = np.ogrid[0:6.01, 0:6.01, 0:6.01, 0:4]
```

### Step 2: Assign data = value

```python
data = ell + m + n + o
```

### Step 3: Assign nni = NearestNeighborInterpolator(...)

```python
nni = NearestNeighborInterpolator(data, (1, 1, 1))
```

### Step 4: Assign unknown = value

```python
a, b, c = np.mgrid[0.5:6.5:1.6, 0.5:6.5:2.7, 0.5:6.5:3.8]
```

### Step 5: Call npt.assert_raises()

```python
npt.assert_raises(OutsideImage, nni.__getitem__, (-0.1, 0, 0))
```

### Step 6: Call npt.assert_raises()

```python
npt.assert_raises(OutsideImage, nni.__getitem__, (0, 8.2, 0))
```

### Step 7: Assign x = value

```python
x = a.flat[ii]
```

### Step 8: Assign y = value

```python
y = b.flat[ii]
```

### Step 9: Assign z = value

```python
z = c.flat[ii]
```

### Step 10: Assign expected_result = value

```python
expected_result = int(x) + int(y) + int(z) + o.ravel()
```

### Step 11: Call npt.assert_array_equal()

```python
npt.assert_array_equal(nni[x, y, z], expected_result)
```

### Step 12: Assign ind = np.array(...)

```python
ind = np.array([x, y, z])
```

### Step 13: Call npt.assert_array_equal()

```python
npt.assert_array_equal(nni[ind], expected_result)
```


## Complete Example

```python
# Workflow
ell, m, n, o = np.ogrid[0:6.01, 0:6.01, 0:6.01, 0:4]
data = ell + m + n + o
nni = NearestNeighborInterpolator(data, (1, 1, 1))
a, b, c = np.mgrid[0.5:6.5:1.6, 0.5:6.5:2.7, 0.5:6.5:3.8]
for ii in range(a.size):
    x = a.flat[ii]
    y = b.flat[ii]
    z = c.flat[ii]
    expected_result = int(x) + int(y) + int(z) + o.ravel()
    npt.assert_array_equal(nni[x, y, z], expected_result)
    ind = np.array([x, y, z])
    npt.assert_array_equal(nni[ind], expected_result)
npt.assert_raises(OutsideImage, nni.__getitem__, (-0.1, 0, 0))
npt.assert_raises(OutsideImage, nni.__getitem__, (0, 8.2, 0))
```

## Next Steps


---

*Source: test_interpolation.py:309 | Complexity: Advanced | Last updated: 2026-05-18*