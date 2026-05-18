# How To: Unique Edges

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test unique edges

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

### Step 1: Assign faces = np.array(...)

```python
faces = np.array([[0, 1, 2], [1, 2, 0]])
```

### Step 2: Assign e = array_to_set(...)

```python
e = array_to_set([[1, 2], [0, 1], [0, 2]])
```

### Step 3: Assign u = unique_edges(...)

```python
u = unique_edges(faces)
```

### Step 4: Call nt.assert_equal()

```python
nt.assert_equal(e, array_to_set(u))
```

### Step 5: Assign unknown = unique_edges(...)

```python
u, m = unique_edges(faces, return_mapping=True)
```

### Step 6: Call nt.assert_equal()

```python
nt.assert_equal(e, array_to_set(u))
```

### Step 7: Assign edges = value

```python
edges = [[[0, 1], [1, 2], [2, 0]], [[1, 2], [2, 0], [0, 1]]]
```

### Step 8: Call nt.assert_equal()

```python
nt.assert_equal(np.sort(u[m], -1), np.sort(edges, -1))
```


## Complete Example

```python
# Workflow
faces = np.array([[0, 1, 2], [1, 2, 0]])
e = array_to_set([[1, 2], [0, 1], [0, 2]])
u = unique_edges(faces)
nt.assert_equal(e, array_to_set(u))
u, m = unique_edges(faces, return_mapping=True)
nt.assert_equal(e, array_to_set(u))
edges = [[[0, 1], [1, 2], [2, 0]], [[1, 2], [2, 0], [0, 1]]]
nt.assert_equal(np.sort(u[m], -1), np.sort(edges, -1))
```

## Next Steps


---

*Source: test_sphere.py:78 | Complexity: Advanced | Last updated: 2026-05-18*