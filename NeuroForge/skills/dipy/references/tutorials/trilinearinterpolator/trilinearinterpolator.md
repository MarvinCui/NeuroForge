# How To: Trilinearinterpolator

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test TriLinearInterpolator

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
ell, m, n, o = np.ogrid[0.5:6.51, 0.5:6.51, 0.5:6.51, 0:4]
```

### Step 2: Assign data = value

```python
data = ell + m + n + o
```

### Step 3: Assign data = data.astype(...)

```python
data = data.astype('float32')
```

### Step 4: Assign tli = TriLinearInterpolator(...)

```python
tli = TriLinearInterpolator(data, (1, 1, 1))
```

### Step 5: Assign unknown = value

```python
a, b, c = np.mgrid[0.5:6.5:1.6, 0.5:6.5:2.7, 0.5:6.5:3.8]
```

### Step 6: Assign expected_value = value

```python
expected_value = np.arange(4) + 1.5
```

### Step 7: Call npt.assert_array_almost_equal()

```python
npt.assert_array_almost_equal(tli[0, 0, 0], expected_value)
```

### Step 8: Assign expected_value = value

```python
expected_value = np.arange(4) + 6.5 * 3
```

### Step 9: Call npt.assert_array_almost_equal()

```python
npt.assert_array_almost_equal(tli[7, 7, 7], expected_value)
```

### Step 10: Call npt.assert_raises()

```python
npt.assert_raises(OutsideImage, tli.__getitem__, (-0.1, 0, 0))
```

### Step 11: Call npt.assert_raises()

```python
npt.assert_raises(OutsideImage, tli.__getitem__, (0, 7.01, 0))
```

### Step 12: Assign x = value

```python
x = a.flat[ii]
```

### Step 13: Assign y = value

```python
y = b.flat[ii]
```

### Step 14: Assign z = value

```python
z = c.flat[ii]
```

### Step 15: Assign expected_result = value

```python
expected_result = x + y + z + o.ravel()
```

### Step 16: Call npt.assert_array_almost_equal()

```python
npt.assert_array_almost_equal(tli[x, y, z], expected_result, decimal=5)
```

### Step 17: Assign ind = np.array(...)

```python
ind = np.array([x, y, z])
```

### Step 18: Call npt.assert_array_almost_equal()

```python
npt.assert_array_almost_equal(tli[ind], expected_result)
```


## Complete Example

```python
# Workflow
ell, m, n, o = np.ogrid[0.5:6.51, 0.5:6.51, 0.5:6.51, 0:4]
data = ell + m + n + o
data = data.astype('float32')
tli = TriLinearInterpolator(data, (1, 1, 1))
a, b, c = np.mgrid[0.5:6.5:1.6, 0.5:6.5:2.7, 0.5:6.5:3.8]
for ii in range(a.size):
    x = a.flat[ii]
    y = b.flat[ii]
    z = c.flat[ii]
    expected_result = x + y + z + o.ravel()
    npt.assert_array_almost_equal(tli[x, y, z], expected_result, decimal=5)
    ind = np.array([x, y, z])
    npt.assert_array_almost_equal(tli[ind], expected_result)
expected_value = np.arange(4) + 1.5
npt.assert_array_almost_equal(tli[0, 0, 0], expected_value)
expected_value = np.arange(4) + 6.5 * 3
npt.assert_array_almost_equal(tli[7, 7, 7], expected_value)
npt.assert_raises(OutsideImage, tli.__getitem__, (-0.1, 0, 0))
npt.assert_raises(OutsideImage, tli.__getitem__, (0, 7.01, 0))
```

## Next Steps


---

*Source: test_interpolation.py:328 | Complexity: Advanced | Last updated: 2026-05-18*