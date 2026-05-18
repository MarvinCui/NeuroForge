# How To: Polar To Cartesian

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test helper transform function from polar to cartesian.

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

### Step 1: 'Test helper transform function from polar to cartesian.'

```python
'Test helper transform function from polar to cartesian.'
```

**Verification:**
```python
assert_allclose(coord, (x, y), atol=1e-07)
```

### Step 2: Assign r = 1

```python
r = 1
```

**Verification:**
```python
assert_allclose(coord, (-1, 0), atol=1e-07)
```

### Step 3: Assign theta = value

```python
theta = np.pi
```

**Verification:**
```python
assert_allclose(coord, _polar_to_cartesian(theta, r), atol=1e-07)
```

### Step 4: Assign x = value

```python
x = r * np.cos(theta)
```

**Verification:**
```python
assert_allclose([_polar_to_cartesian(p[1], p[0]) for p in polar], _pol_to_cart(polar), atol=1e-07)
```

### Step 5: Assign y = value

```python
y = r * np.sin(theta)
```

### Step 6: Assign coord = value

```python
coord = _pol_to_cart(np.array([[r, theta]]))[0]
```

### Step 7: Call assert_allclose()

```python
assert_allclose(coord, (x, y), atol=1e-07)
```

### Step 8: Call assert_allclose()

```python
assert_allclose(coord, (-1, 0), atol=1e-07)
```

### Step 9: Call assert_allclose()

```python
assert_allclose(coord, _polar_to_cartesian(theta, r), atol=1e-07)
```

### Step 10: Assign rng = np.random.RandomState(...)

```python
rng = np.random.RandomState(0)
```

### Step 11: Assign r = rng.randn(...)

```python
r = rng.randn(10)
```

### Step 12: Assign theta = value

```python
theta = rng.rand(10) * (2 * np.pi)
```

### Step 13: Assign polar = value

```python
polar = np.array((r, theta)).T
```

### Step 14: Call assert_allclose()

```python
assert_allclose([_polar_to_cartesian(p[1], p[0]) for p in polar], _pol_to_cart(polar), atol=1e-07)
```


## Complete Example

```python
# Workflow
'Test helper transform function from polar to cartesian.'
r = 1
theta = np.pi
x = r * np.cos(theta)
y = r * np.sin(theta)
coord = _pol_to_cart(np.array([[r, theta]]))[0]
assert_allclose(coord, (x, y), atol=1e-07)
assert_allclose(coord, (-1, 0), atol=1e-07)
assert_allclose(coord, _polar_to_cartesian(theta, r), atol=1e-07)
rng = np.random.RandomState(0)
r = rng.randn(10)
theta = rng.rand(10) * (2 * np.pi)
polar = np.array((r, theta)).T
assert_allclose([_polar_to_cartesian(p[1], p[0]) for p in polar], _pol_to_cart(polar), atol=1e-07)
```

## Next Steps


---

*Source: test_transforms.py:208 | Complexity: Advanced | Last updated: 2026-05-18*