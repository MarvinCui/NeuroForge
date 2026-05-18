# How To: Tps

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test TPS warping.

## Prerequisites

**Required Modules:**
- `itertools`
- `os`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne`
- `mne.datasets`
- `mne.fixes`
- `mne.io`
- `mne.transforms`
- `mne.transforms`
- `dipy.align`


## Step-by-Step Guide

### Step 1: 'Test TPS warping.'

```python
'Test TPS warping.'
```

**Verification:**
```python
assert_equal(sph.shape[1], 200)
```

### Step 2: Assign az = np.linspace(...)

```python
az = np.linspace(0.0, 2 * np.pi, 20, endpoint=False)
```

**Verification:**
```python
assert 'no ' in repr(warp)
```

### Step 3: Assign pol = value

```python
pol = np.linspace(0, np.pi, 12)[1:-1]
```

**Verification:**
```python
assert 'oct5' in repr(warp)
```

### Step 4: Assign sph = np.array(...)

```python
sph = np.array(np.meshgrid(1, az, pol, indexing='ij'))
```

**Verification:**
```python
assert_allclose(destination_est, destination, atol=0.001)
```

### Step 5: Assign sph = _reshape_view(...)

```python
sph = _reshape_view(sph, (3, -1))
```

### Step 6: Call assert_equal()

```python
assert_equal(sph.shape[1], 200)
```

### Step 7: Assign source = _sph_to_cart(...)

```python
source = _sph_to_cart(sph.T)
```

### Step 8: Assign destination = source.copy(...)

```python
destination = source.copy()
```

### Step 9: Assign warp = SphericalSurfaceWarp(...)

```python
warp = SphericalSurfaceWarp()
```

**Verification:**
```python
assert 'no ' in repr(warp)
```

### Step 10: Call warp.fit()

```python
warp.fit(source[::3], destination[::2])
```

**Verification:**
```python
assert 'oct5' in repr(warp)
```

### Step 11: Assign destination_est = warp.transform(...)

```python
destination_est = warp.transform(source)
```

### Step 12: Call assert_allclose()

```python
assert_allclose(destination_est, destination, atol=0.001)
```


## Complete Example

```python
# Workflow
'Test TPS warping.'
az = np.linspace(0.0, 2 * np.pi, 20, endpoint=False)
pol = np.linspace(0, np.pi, 12)[1:-1]
sph = np.array(np.meshgrid(1, az, pol, indexing='ij'))
sph = _reshape_view(sph, (3, -1))
assert_equal(sph.shape[1], 200)
source = _sph_to_cart(sph.T)
destination = source.copy()
destination *= 2
destination[:, 0] += 1
warp = SphericalSurfaceWarp()
assert 'no ' in repr(warp)
warp.fit(source[::3], destination[::2])
assert 'oct5' in repr(warp)
destination_est = warp.transform(source)
assert_allclose(destination_est, destination, atol=0.001)
```

## Next Steps


---

*Source: test_transforms.py:74 | Complexity: Advanced | Last updated: 2026-05-18*