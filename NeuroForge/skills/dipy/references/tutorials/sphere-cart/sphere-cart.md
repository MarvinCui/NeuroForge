# How To: Sphere Cart

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test sphere cart

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

### Step 1: Assign unknown = cart2sphere(...)

```python
rs, thetas, phis = cart2sphere(*sphere_points.T)
```

**Verification:**
```python
assert_array_almost_equal(xyz, sphere_points.T)
```

### Step 2: Assign xyz = sphere2cart(...)

```python
xyz = sphere2cart(rs, thetas, phis)
```

**Verification:**
```python
assert_array_almost_equal(rs, 10.4)
```

### Step 3: Call assert_array_almost_equal()

```python
assert_array_almost_equal(xyz, sphere_points.T)
```

**Verification:**
```python
assert_array_almost_equal(xyz, big_sph_pts.T, decimal=6)
```

### Step 4: Assign big_sph_pts = value

```python
big_sph_pts = sphere_points * 10.4
```

**Verification:**
```python
assert_equal(r.shape, theta.shape)
```

### Step 5: Assign unknown = cart2sphere(...)

```python
rs, thetas, phis = cart2sphere(*big_sph_pts.T)
```

**Verification:**
```python
assert_equal(r.shape, phi.shape)
```

### Step 6: Call assert_array_almost_equal()

```python
assert_array_almost_equal(rs, 10.4)
```

**Verification:**
```python
assert_equal(x.shape, y.shape)
```

### Step 7: Assign xyz = sphere2cart(...)

```python
xyz = sphere2cart(rs, thetas, phis)
```

**Verification:**
```python
assert_equal(x.shape, z.shape)
```

### Step 8: Call assert_array_almost_equal()

```python
assert_array_almost_equal(xyz, big_sph_pts.T, decimal=6)
```

**Verification:**
```python
assert_array_almost_equal(xyz, pt)
```

### Step 9: Assign unknown = value

```python
x, y, z = big_sph_pts.T
```

**Verification:**
```python
assert_array_almost_equal((x, y, z), (1.0, 1.0, 1.0))
```

### Step 10: Assign unknown = cart2sphere(...)

```python
r, theta, phi = cart2sphere(x[:1], y[:1], z)
```

### Step 11: Call assert_equal()

```python
assert_equal(r.shape, theta.shape)
```

### Step 12: Call assert_equal()

```python
assert_equal(r.shape, phi.shape)
```

### Step 13: Assign unknown = sphere2cart(...)

```python
x, y, z = sphere2cart(r[:1], theta[:1], phi)
```

### Step 14: Call assert_equal()

```python
assert_equal(x.shape, y.shape)
```

### Step 15: Call assert_equal()

```python
assert_equal(x.shape, z.shape)
```

### Step 16: Assign pt = value

```python
pt = sphere_points[3]
```

### Step 17: Assign unknown = cart2sphere(...)

```python
r, theta, phi = cart2sphere(*pt)
```

### Step 18: Assign xyz = sphere2cart(...)

```python
xyz = sphere2cart(r, theta, phi)
```

### Step 19: Call assert_array_almost_equal()

```python
assert_array_almost_equal(xyz, pt)
```

### Step 20: Assign unknown = sphere2cart(...)

```python
x, y, z = sphere2cart(*cart2sphere(1.0, 1.0, 1.0))
```

### Step 21: Call assert_array_almost_equal()

```python
assert_array_almost_equal((x, y, z), (1.0, 1.0, 1.0))
```


## Complete Example

```python
# Workflow
rs, thetas, phis = cart2sphere(*sphere_points.T)
xyz = sphere2cart(rs, thetas, phis)
assert_array_almost_equal(xyz, sphere_points.T)
big_sph_pts = sphere_points * 10.4
rs, thetas, phis = cart2sphere(*big_sph_pts.T)
assert_array_almost_equal(rs, 10.4)
xyz = sphere2cart(rs, thetas, phis)
assert_array_almost_equal(xyz, big_sph_pts.T, decimal=6)
x, y, z = big_sph_pts.T
r, theta, phi = cart2sphere(x[:1], y[:1], z)
assert_equal(r.shape, theta.shape)
assert_equal(r.shape, phi.shape)
x, y, z = sphere2cart(r[:1], theta[:1], phi)
assert_equal(x.shape, y.shape)
assert_equal(x.shape, z.shape)
pt = sphere_points[3]
r, theta, phi = cart2sphere(*pt)
xyz = sphere2cart(r, theta, phi)
assert_array_almost_equal(xyz, pt)
x, y, z = sphere2cart(*cart2sphere(1.0, 1.0, 1.0))
assert_array_almost_equal((x, y, z), (1.0, 1.0, 1.0))
```

## Next Steps


---

*Source: test_geometry.py:47 | Complexity: Advanced | Last updated: 2026-05-18*