# How To: Invert Transform

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test invert transform

## Prerequisites

**Required Modules:**
- `itertools`
- `random`
- `numpy`
- `numpy.testing`
- `dipy.core.geometry`
- `dipy.core.sphere_stats`
- `dipy.testing.decorators`
- `dipy.testing.spherepoints`


## Step-by-Step Guide

### Step 1: Assign n = 100.0

```python
n = 100.0
```

**Verification:**
```python
assert_array_almost_equal(theta, new_theta)
```

### Step 2: Assign theta = value

```python
theta = np.arange(n) / n * np.pi
```

**Verification:**
```python
assert_array_almost_equal(phi, new_phi)
```

### Step 3: Assign phi = value

```python
phi = (np.arange(n) / n - 0.5) * 2 * np.pi
```

### Step 4: Assign unknown = sphere2cart(...)

```python
x, y, z = sphere2cart(1, theta, phi)
```

### Step 5: Assign unknown = cart2sphere(...)

```python
r, new_theta, new_phi = cart2sphere(x, y, z)
```

### Step 6: Call assert_array_almost_equal()

```python
assert_array_almost_equal(theta, new_theta)
```

### Step 7: Call assert_array_almost_equal()

```python
assert_array_almost_equal(phi, new_phi)
```


## Complete Example

```python
# Workflow
n = 100.0
theta = np.arange(n) / n * np.pi
phi = (np.arange(n) / n - 0.5) * 2 * np.pi
x, y, z = sphere2cart(1, theta, phi)
r, new_theta, new_phi = cart2sphere(x, y, z)
assert_array_almost_equal(theta, new_theta)
assert_array_almost_equal(phi, new_phi)
```

## Next Steps


---

*Source: test_geometry.py:77 | Complexity: Intermediate | Last updated: 2026-05-18*