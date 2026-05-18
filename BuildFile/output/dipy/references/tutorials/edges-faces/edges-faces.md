# How To: Edges Faces

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test edges faces

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

### Step 1: Assign s = Sphere(...)

```python
s = Sphere(xyz=verts)
```

### Step 2: Assign faces = oct_faces

```python
faces = oct_faces
```

### Step 3: Call nt.assert_equal()

```python
nt.assert_equal(array_to_set(s.faces), array_to_set(faces))
```

### Step 4: Call nt.assert_equal()

```python
nt.assert_equal(array_to_set(s.edges), array_to_set(edges))
```

### Step 5: Assign s = Sphere(...)

```python
s = Sphere(xyz=verts, faces=[[0, 1, 2]])
```

### Step 6: Call nt.assert_equal()

```python
nt.assert_equal(array_to_set(s.faces), array_to_set([[0, 1, 2]]))
```

### Step 7: Call nt.assert_equal()

```python
nt.assert_equal(array_to_set(s.edges), array_to_set([[0, 1], [1, 2], [0, 2]]))
```

### Step 8: Assign s = Sphere(...)

```python
s = Sphere(xyz=verts, faces=[[0, 1, 2]], edges=[[0, 1]])
```

### Step 9: Call nt.assert_equal()

```python
nt.assert_equal(array_to_set(s.faces), array_to_set([[0, 1, 2]]))
```

### Step 10: Call nt.assert_equal()

```python
nt.assert_equal(array_to_set(s.edges), array_to_set([[0, 1]]))
```


## Complete Example

```python
# Workflow
s = Sphere(xyz=verts)
faces = oct_faces
nt.assert_equal(array_to_set(s.faces), array_to_set(faces))
nt.assert_equal(array_to_set(s.edges), array_to_set(edges))
s = Sphere(xyz=verts, faces=[[0, 1, 2]])
nt.assert_equal(array_to_set(s.faces), array_to_set([[0, 1, 2]]))
nt.assert_equal(array_to_set(s.edges), array_to_set([[0, 1], [1, 2], [0, 2]]))
s = Sphere(xyz=verts, faces=[[0, 1, 2]], edges=[[0, 1]])
nt.assert_equal(array_to_set(s.faces), array_to_set([[0, 1, 2]]))
nt.assert_equal(array_to_set(s.edges), array_to_set([[0, 1]]))
```

## Next Steps


---

*Source: test_sphere.py:122 | Complexity: Advanced | Last updated: 2026-05-18*