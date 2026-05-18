# How To: Sphere Subdivide

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test sphere subdivide

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `dipy.core.geometry`
- `dipy.core.sphere`
- `dipy.core.sphere_stats`
- `dipy.testing.decorators`


## Step-by-Step Guide

### Step 1: Assign sphere1 = unit_octahedron.subdivide(...)

```python
sphere1 = unit_octahedron.subdivide(n=4)
```

### Step 2: Assign sphere2 = Sphere(...)

```python
sphere2 = Sphere(xyz=sphere1.vertices)
```

### Step 3: Call nt.assert_equal()

```python
nt.assert_equal(sphere1.faces.shape, sphere2.faces.shape)
```

### Step 4: Call nt.assert_equal()

```python
nt.assert_equal(array_to_set(sphere1.faces), array_to_set(sphere2.faces))
```

### Step 5: Assign sphere1 = unit_icosahedron.subdivide(...)

```python
sphere1 = unit_icosahedron.subdivide(n=4)
```

### Step 6: Assign sphere2 = Sphere(...)

```python
sphere2 = Sphere(xyz=sphere1.vertices)
```

### Step 7: Call nt.assert_equal()

```python
nt.assert_equal(sphere1.faces.shape, sphere2.faces.shape)
```

### Step 8: Call nt.assert_equal()

```python
nt.assert_equal(array_to_set(sphere1.faces), array_to_set(sphere2.faces))
```


## Complete Example

```python
# Workflow
sphere1 = unit_octahedron.subdivide(n=4)
sphere2 = Sphere(xyz=sphere1.vertices)
nt.assert_equal(sphere1.faces.shape, sphere2.faces.shape)
nt.assert_equal(array_to_set(sphere1.faces), array_to_set(sphere2.faces))
sphere1 = unit_icosahedron.subdivide(n=4)
sphere2 = Sphere(xyz=sphere1.vertices)
nt.assert_equal(sphere1.faces.shape, sphere2.faces.shape)
nt.assert_equal(array_to_set(sphere1.faces), array_to_set(sphere2.faces))
```

## Next Steps


---

*Source: test_sphere.py:137 | Complexity: Advanced | Last updated: 2026-05-18*