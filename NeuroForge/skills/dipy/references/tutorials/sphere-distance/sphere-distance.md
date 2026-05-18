# How To: Sphere Distance

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test sphere distance

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

### Step 1: Assign radius = 3.2

```python
radius = 3.2
```

**Verification:**
```python
assert_array_almost_equal(cdists, sph_d)
```

### Step 2: Assign n = 5000

```python
n = 5000
```

**Verification:**
```python
assert_array_almost_equal(cdists, sph_d)
```

### Step 3: Assign n2 = value

```python
n2 = n // 2
```

**Verification:**
```python
assert_raises(ValueError, sphere_distance, [1, 0], [0, 2])
```

### Step 4: Assign angles = np.linspace(...)

```python
angles = np.linspace(0, np.pi * 2, n, endpoint=False)
```

**Verification:**
```python
assert_raises(ValueError, sphere_distance, [1, 0], [0, 1], radius=2.0)
```

### Step 5: Assign x = value

```python
x = np.sin(angles) * radius
```

### Step 6: Assign y = value

```python
y = np.cos(angles) * radius
```

### Step 7: Assign half_x = value

```python
half_x = x[:n2 + 1]
```

### Step 8: Assign half_y = value

```python
half_y = y[:n2 + 1]
```

### Step 9: Assign half_dists = np.sqrt(...)

```python
half_dists = np.sqrt(np.diff(half_x) ** 2 + np.diff(half_y) ** 2)
```

### Step 10: Assign csums = np.cumsum(...)

```python
csums = np.cumsum(half_dists)
```

### Step 11: Assign cdists = value

```python
cdists = np.r_[0, csums, csums[-2::-1]]
```

### Step 12: Assign sph_d = sphere_distance(...)

```python
sph_d = sphere_distance([0, radius], np.c_[x, y])
```

### Step 13: Call assert_array_almost_equal()

```python
assert_array_almost_equal(cdists, sph_d)
```

### Step 14: Assign sph_d = sphere_distance(...)

```python
sph_d = sphere_distance([0, radius], np.c_[x, y], radius=radius)
```

### Step 15: Call assert_array_almost_equal()

```python
assert_array_almost_equal(cdists, sph_d)
```

### Step 16: Call assert_raises()

```python
assert_raises(ValueError, sphere_distance, [1, 0], [0, 2])
```

### Step 17: Call sphere_distance()

```python
sphere_distance([1, 0], [0, 2], radius=None, check_radius=False)
```

### Step 18: Call assert_raises()

```python
assert_raises(ValueError, sphere_distance, [1, 0], [0, 1], radius=2.0)
```


## Complete Example

```python
# Workflow
radius = 3.2
n = 5000
n2 = n // 2
angles = np.linspace(0, np.pi * 2, n, endpoint=False)
x = np.sin(angles) * radius
y = np.cos(angles) * radius
half_x = x[:n2 + 1]
half_y = y[:n2 + 1]
half_dists = np.sqrt(np.diff(half_x) ** 2 + np.diff(half_y) ** 2)
csums = np.cumsum(half_dists)
cdists = np.r_[0, csums, csums[-2::-1]]
sph_d = sphere_distance([0, radius], np.c_[x, y])
assert_array_almost_equal(cdists, sph_d)
sph_d = sphere_distance([0, radius], np.c_[x, y], radius=radius)
assert_array_almost_equal(cdists, sph_d)
assert_raises(ValueError, sphere_distance, [1, 0], [0, 2])
sphere_distance([1, 0], [0, 2], radius=None, check_radius=False)
assert_raises(ValueError, sphere_distance, [1, 0], [0, 1], radius=2.0)
```

## Next Steps


---

*Source: test_geometry.py:121 | Complexity: Advanced | Last updated: 2026-05-18*