# How To: Lambert Equal Area Projection Cart

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test lambert equal area projection cart

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

### Step 1: Assign xyz = np.array(...)

```python
xyz = np.array([[1, 0, 0], [0, 1, 0], [0, 0, 1], [-1, 0, 0], [0, -1, 0], [0, 0, -1]])
```

**Verification:**
```python
assert_array_almost_equal(np.sqrt(np.sum(leap ** 2, axis=1)), np.array([r2, r2, 0, r2, r2, 2]))
```

### Step 2: Assign unknown = cart2sphere(...)

```python
r, theta, phi = cart2sphere(*xyz.T)
```

### Step 3: Assign leap = lambert_equal_area_projection_polar(...)

```python
leap = lambert_equal_area_projection_polar(theta, phi)
```

### Step 4: Assign r2 = np.sqrt(...)

```python
r2 = np.sqrt(2)
```

### Step 5: Call assert_array_almost_equal()

```python
assert_array_almost_equal(np.sqrt(np.sum(leap ** 2, axis=1)), np.array([r2, r2, 0, r2, r2, 2]))
```


## Complete Example

```python
# Workflow
xyz = np.array([[1, 0, 0], [0, 1, 0], [0, 0, 1], [-1, 0, 0], [0, -1, 0], [0, 0, -1]])
r, theta, phi = cart2sphere(*xyz.T)
leap = lambert_equal_area_projection_polar(theta, phi)
r2 = np.sqrt(2)
assert_array_almost_equal(np.sqrt(np.sum(leap ** 2, axis=1)), np.array([r2, r2, 0, r2, r2, 2]))
```

## Next Steps


---

*Source: test_geometry.py:191 | Complexity: Intermediate | Last updated: 2026-05-18*