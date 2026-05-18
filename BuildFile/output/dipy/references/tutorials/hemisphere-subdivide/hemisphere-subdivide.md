# How To: Hemisphere Subdivide

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test hemisphere subdivide

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

### Step 1: Assign decimals = 6

```python
decimals = 6
```

### Step 2: Assign hemi1 = HemiSphere.from_sphere.subdivide(...)

```python
hemi1 = HemiSphere.from_sphere(unit_icosahedron).subdivide(n=4)
```

### Step 3: Assign vertices1 = np.round(...)

```python
vertices1 = np.round(hemi1.vertices, decimals)
```

### Step 4: Assign order = np.lexsort(...)

```python
order = np.lexsort(vertices1.T)
```

### Step 5: Assign vertices1 = value

```python
vertices1 = vertices1[order]
```

### Step 6: Assign sphere = unit_icosahedron.subdivide(...)

```python
sphere = unit_icosahedron.subdivide(n=4)
```

### Step 7: Assign hemi2 = HemiSphere.from_sphere(...)

```python
hemi2 = HemiSphere.from_sphere(sphere)
```

### Step 8: Assign vertices2 = np.round(...)

```python
vertices2 = np.round(hemi2.vertices, decimals)
```

### Step 9: Assign order = np.lexsort(...)

```python
order = np.lexsort(vertices2.T)
```

### Step 10: Assign vertices2 = value

```python
vertices2 = vertices2[order]
```

### Step 11: Call nt.assert_array_equal()

```python
nt.assert_array_equal(vertices1, vertices2)
```

### Step 12: Assign hemi3 = HemiSphere(...)

```python
hemi3 = HemiSphere(xyz=hemi1.vertices)
```

### Step 13: Call nt.assert_array_equal()

```python
nt.assert_array_equal(hemi1.faces, hemi3.faces)
```

### Step 14: Call nt.assert_array_equal()

```python
nt.assert_array_equal(hemi1.edges, hemi3.edges)
```

### Step 15: Assign unknown = value

```python
x, y, z = vertices.T
```

### Step 16: Assign f = value

```python
f = (z < 0) | (z == 0) & (y < 0) | (z == 0) & (y == 0) & (x < 0)
```


## Complete Example

```python
# Workflow
def flip(vertices):
    x, y, z = vertices.T
    f = (z < 0) | (z == 0) & (y < 0) | (z == 0) & (y == 0) & (x < 0)
    return 1 - 2 * f[:, None]
decimals = 6
hemi1 = HemiSphere.from_sphere(unit_icosahedron).subdivide(n=4)
vertices1 = np.round(hemi1.vertices, decimals)
vertices1 *= flip(vertices1)
order = np.lexsort(vertices1.T)
vertices1 = vertices1[order]
sphere = unit_icosahedron.subdivide(n=4)
hemi2 = HemiSphere.from_sphere(sphere)
vertices2 = np.round(hemi2.vertices, decimals)
vertices2 *= flip(vertices2)
order = np.lexsort(vertices2.T)
vertices2 = vertices2[order]
nt.assert_array_equal(vertices1, vertices2)
hemi3 = HemiSphere(xyz=hemi1.vertices)
nt.assert_array_equal(hemi1.faces, hemi3.faces)
nt.assert_array_equal(hemi1.edges, hemi3.edges)
```

## Next Steps


---

*Source: test_sphere.py:166 | Complexity: Advanced | Last updated: 2026-05-18*