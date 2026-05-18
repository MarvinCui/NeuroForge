# How To: Topo To Sph

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test topo to sphere conversion.

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

### Step 1: 'Test topo to sphere conversion.'

```python
'Test topo to sphere conversion.'
```

**Verification:**
```python
assert_allclose(_topo_to_phi_theta(angle, radius), [45, -30])
```

### Step 2: Assign rng = np.random.RandomState(...)

```python
rng = np.random.RandomState(0)
```

**Verification:**
```python
assert_allclose(sph[ii], [1.0, azimuth, np.pi / 2.0 - elevation], atol=1e-07)
```

### Step 3: Assign angles = value

```python
angles = rng.rand(10) * 360
```

**Verification:**
```python
assert_allclose(pos, expected, atol=1e-07)
```

### Step 4: Assign radii = rng.rand(...)

```python
radii = rng.rand(10)
```

**Verification:**
```python
assert_allclose(pos, new[ii], atol=1e-07)
```

### Step 5: Assign unknown = 30

```python
angles[0] = 30
```

### Step 6: Assign unknown = 0.25

```python
radii[0] = 0.25
```

### Step 7: Assign sph = _topo_to_sph(...)

```python
sph = _topo_to_sph(np.array([angles, radii]).T)
```

### Step 8: Assign new = _sph_to_cart(...)

```python
new = _sph_to_cart(sph)
```

### Step 9: Assign unknown = value

```python
new[:, [0, 1]] = new[:, [1, 0]] * [-1, 1]
```

### Step 10: Assign unknown = _topo_to_phi_theta(...)

```python
sph_phi, sph_theta = _topo_to_phi_theta(angle, radius)
```

### Step 11: Assign azimuth = value

```python
azimuth = sph_theta / 180.0 * np.pi
```

### Step 12: Assign elevation = value

```python
elevation = sph_phi / 180.0 * np.pi
```

### Step 13: Call assert_allclose()

```python
assert_allclose(sph[ii], [1.0, azimuth, np.pi / 2.0 - elevation], atol=1e-07)
```

### Step 14: Assign r = np.ones_like(...)

```python
r = np.ones_like(radius)
```

### Step 15: Assign unknown = _sphere_to_cartesian(...)

```python
x, y, z = _sphere_to_cartesian(azimuth, elevation, r)
```

### Step 16: Assign pos = value

```python
pos = [-y, x, z]
```

### Step 17: Call assert_allclose()

```python
assert_allclose(pos, new[ii], atol=1e-07)
```

### Step 18: Call assert_allclose()

```python
assert_allclose(_topo_to_phi_theta(angle, radius), [45, -30])
```

### Step 19: Assign expected = np.array(...)

```python
expected = np.array([1.0 / 2.0, np.sqrt(3) / 2.0, 1.0])
```

### Step 20: Call assert_allclose()

```python
assert_allclose(pos, expected, atol=1e-07)
```


## Complete Example

```python
# Workflow
'Test topo to sphere conversion.'
rng = np.random.RandomState(0)
angles = rng.rand(10) * 360
radii = rng.rand(10)
angles[0] = 30
radii[0] = 0.25
sph = _topo_to_sph(np.array([angles, radii]).T)
new = _sph_to_cart(sph)
new[:, [0, 1]] = new[:, [1, 0]] * [-1, 1]
for ii, (angle, radius) in enumerate(zip(angles, radii)):
    sph_phi, sph_theta = _topo_to_phi_theta(angle, radius)
    if ii == 0:
        assert_allclose(_topo_to_phi_theta(angle, radius), [45, -30])
    azimuth = sph_theta / 180.0 * np.pi
    elevation = sph_phi / 180.0 * np.pi
    assert_allclose(sph[ii], [1.0, azimuth, np.pi / 2.0 - elevation], atol=1e-07)
    r = np.ones_like(radius)
    x, y, z = _sphere_to_cartesian(azimuth, elevation, r)
    pos = [-y, x, z]
    if ii == 0:
        expected = np.array([1.0 / 2.0, np.sqrt(3) / 2.0, 1.0])
        expected /= np.sqrt(2)
        assert_allclose(pos, expected, atol=1e-07)
    assert_allclose(pos, new[ii], atol=1e-07)
```

## Next Steps


---

*Source: test_transforms.py:236 | Complexity: Advanced | Last updated: 2026-05-18*