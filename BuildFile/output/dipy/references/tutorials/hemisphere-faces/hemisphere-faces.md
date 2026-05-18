# How To: Hemisphere Faces

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test hemisphere faces

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

### Step 1: Assign t = value

```python
t = (1 + np.sqrt(5)) / 2
```

### Step 2: Assign vertices = np.array(...)

```python
vertices = np.array([[-t, -1, 0], [-t, 1, 0], [1, 0, t], [-1, 0, t], [0, t, 1], [0, -t, 1]])
```

### Step 3: Assign faces = np.array(...)

```python
faces = np.array([[0, 1, 2], [0, 1, 3], [0, 2, 4], [1, 3, 4], [2, 3, 4], [1, 2, 5], [0, 3, 5], [2, 3, 5], [0, 4, 5], [1, 4, 5]])
```

### Step 4: Assign edges = np.array(...)

```python
edges = np.array([(0, 1), (0, 2), (0, 3), (0, 4), (0, 5), (1, 2), (1, 3), (1, 4), (1, 5), (2, 3), (2, 4), (2, 5), (3, 4), (3, 5), (4, 5)])
```

### Step 5: Assign h = HemiSphere(...)

```python
h = HemiSphere(xyz=vertices)
```

### Step 6: Call nt.assert_equal()

```python
nt.assert_equal(len(h.edges), len(edges))
```

### Step 7: Call nt.assert_equal()

```python
nt.assert_equal(array_to_set(h.edges), array_to_set(edges))
```

### Step 8: Call nt.assert_equal()

```python
nt.assert_equal(len(h.faces), len(faces))
```

### Step 9: Call nt.assert_equal()

```python
nt.assert_equal(array_to_set(h.faces), array_to_set(faces))
```


## Complete Example

```python
# Workflow
t = (1 + np.sqrt(5)) / 2
vertices = np.array([[-t, -1, 0], [-t, 1, 0], [1, 0, t], [-1, 0, t], [0, t, 1], [0, -t, 1]])
vertices /= vector_norm(vertices, keepdims=True)
faces = np.array([[0, 1, 2], [0, 1, 3], [0, 2, 4], [1, 3, 4], [2, 3, 4], [1, 2, 5], [0, 3, 5], [2, 3, 5], [0, 4, 5], [1, 4, 5]])
edges = np.array([(0, 1), (0, 2), (0, 3), (0, 4), (0, 5), (1, 2), (1, 3), (1, 4), (1, 5), (2, 3), (2, 4), (2, 5), (3, 4), (3, 5), (4, 5)])
h = HemiSphere(xyz=vertices)
nt.assert_equal(len(h.edges), len(edges))
nt.assert_equal(array_to_set(h.edges), array_to_set(edges))
nt.assert_equal(len(h.faces), len(faces))
nt.assert_equal(array_to_set(h.faces), array_to_set(faces))
```

## Next Steps


---

*Source: test_sphere.py:240 | Complexity: Advanced | Last updated: 2026-05-18*