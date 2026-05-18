# How To: Sph To Cart

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test conversion between sphere and cartesian.

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

### Step 1: 'Test conversion between sphere and cartesian.'

```python
'Test conversion between sphere and cartesian.'
```

**Verification:**
```python
assert_allclose(coord, (x, y, z), atol=1e-07)
```

### Step 2: Assign unknown = value

```python
r, theta, phi = (11.0, 0.0, np.pi / 2.0)
```

**Verification:**
```python
assert_allclose(coord, (r, 0, 0), atol=1e-07)
```

### Step 3: Assign z = value

```python
z = r * np.cos(phi)
```

**Verification:**
```python
assert_allclose(_sph_to_cart(_cart_to_sph(coords)), coords, atol=1e-05)
```

### Step 4: Assign rsin_phi = value

```python
rsin_phi = r * np.sin(phi)
```

**Verification:**
```python
assert_allclose(sph[0], sph_old[[2, 0, 1]], atol=1e-07)
```

### Step 5: Assign x = value

```python
x = rsin_phi * np.cos(theta)
```

**Verification:**
```python
assert_allclose(cart[0], cart_old, atol=1e-07)
```

### Step 6: Assign y = value

```python
y = rsin_phi * np.sin(theta)
```

**Verification:**
```python
assert_allclose(cart[0], coord, atol=1e-07)
```

### Step 7: Assign coord = value

```python
coord = _sph_to_cart(np.array([[r, theta, phi]]))[0]
```

### Step 8: Call assert_allclose()

```python
assert_allclose(coord, (x, y, z), atol=1e-07)
```

### Step 9: Call assert_allclose()

```python
assert_allclose(coord, (r, 0, 0), atol=1e-07)
```

### Step 10: Assign rng = np.random.RandomState(...)

```python
rng = np.random.RandomState(0)
```

### Step 11: Assign coords = rng.randn(...)

```python
coords = rng.randn(10, 3)
```

### Step 12: Call assert_allclose()

```python
assert_allclose(_sph_to_cart(_cart_to_sph(coords)), coords, atol=1e-05)
```

### Step 13: Assign sph = _cart_to_sph(...)

```python
sph = _cart_to_sph(coord[np.newaxis])
```

### Step 14: Assign cart = _sph_to_cart(...)

```python
cart = _sph_to_cart(sph)
```

### Step 15: Assign sph_old = np.array(...)

```python
sph_old = np.array(_cartesian_to_sphere(*coord))
```

### Step 16: Assign cart_old = _sphere_to_cartesian(...)

```python
cart_old = _sphere_to_cartesian(*sph_old)
```

### Step 17: Assign unknown = value

```python
sph_old[1] = np.pi / 2.0 - sph_old[1]
```

### Step 18: Call assert_allclose()

```python
assert_allclose(sph[0], sph_old[[2, 0, 1]], atol=1e-07)
```

### Step 19: Call assert_allclose()

```python
assert_allclose(cart[0], cart_old, atol=1e-07)
```

### Step 20: Call assert_allclose()

```python
assert_allclose(cart[0], coord, atol=1e-07)
```


## Complete Example

```python
# Workflow
'Test conversion between sphere and cartesian.'
r, theta, phi = (11.0, 0.0, np.pi / 2.0)
z = r * np.cos(phi)
rsin_phi = r * np.sin(phi)
x = rsin_phi * np.cos(theta)
y = rsin_phi * np.sin(theta)
coord = _sph_to_cart(np.array([[r, theta, phi]]))[0]
assert_allclose(coord, (x, y, z), atol=1e-07)
assert_allclose(coord, (r, 0, 0), atol=1e-07)
rng = np.random.RandomState(0)
coords = rng.randn(10, 3)
assert_allclose(_sph_to_cart(_cart_to_sph(coords)), coords, atol=1e-05)
for coord in coords:
    sph = _cart_to_sph(coord[np.newaxis])
    cart = _sph_to_cart(sph)
    sph_old = np.array(_cartesian_to_sphere(*coord))
    cart_old = _sphere_to_cartesian(*sph_old)
    sph_old[1] = np.pi / 2.0 - sph_old[1]
    assert_allclose(sph[0], sph_old[[2, 0, 1]], atol=1e-07)
    assert_allclose(cart[0], cart_old, atol=1e-07)
    assert_allclose(cart[0], coord, atol=1e-07)
```

## Next Steps


---

*Source: test_transforms.py:174 | Complexity: Advanced | Last updated: 2026-05-18*