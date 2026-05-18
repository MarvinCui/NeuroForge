# How To: Mirror

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test mirror

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

### Step 1: Assign verts = value

```python
verts = [[0, 0, 1], [0, 1, 0], [1, 0, 0], [-1, -1, -1]]
```

### Step 2: Assign verts = np.array(...)

```python
verts = np.array(verts, 'float')
```

### Step 3: Assign verts = value

```python
verts = verts / np.sqrt((verts * verts).sum(-1)[:, None])
```

### Step 4: Assign faces = value

```python
faces = [[0, 1, 3], [0, 2, 3], [1, 2, 3]]
```

### Step 5: Assign h = HemiSphere(...)

```python
h = HemiSphere(xyz=verts, faces=faces)
```

### Step 6: Assign s = h.mirror(...)

```python
s = h.mirror()
```

### Step 7: Call nt.assert_equal()

```python
nt.assert_equal(len(s.vertices), 8)
```

### Step 8: Call nt.assert_equal()

```python
nt.assert_equal(len(s.faces), 6)
```

### Step 9: Assign verts = value

```python
verts = s.vertices
```

### Step 10: Assign unknown = triangle

```python
a, b, c = triangle
```

### Step 11: Call nt.assert_()

```python
nt.assert_(_angle(verts[a], verts[b]) <= np.pi / 2)
```

### Step 12: Call nt.assert_()

```python
nt.assert_(_angle(verts[a], verts[c]) <= np.pi / 2)
```

### Step 13: Call nt.assert_()

```python
nt.assert_(_angle(verts[b], verts[c]) <= np.pi / 2)
```


## Complete Example

```python
# Workflow
verts = [[0, 0, 1], [0, 1, 0], [1, 0, 0], [-1, -1, -1]]
verts = np.array(verts, 'float')
verts = verts / np.sqrt((verts * verts).sum(-1)[:, None])
faces = [[0, 1, 3], [0, 2, 3], [1, 2, 3]]
h = HemiSphere(xyz=verts, faces=faces)
s = h.mirror()
nt.assert_equal(len(s.vertices), 8)
nt.assert_equal(len(s.faces), 6)
verts = s.vertices

def _angle(a, b):
    return np.arccos(np.dot(a, b))
for triangle in s.faces:
    a, b, c = triangle
    nt.assert_(_angle(verts[a], verts[b]) <= np.pi / 2)
    nt.assert_(_angle(verts[a], verts[c]) <= np.pi / 2)
    nt.assert_(_angle(verts[b], verts[c]) <= np.pi / 2)
```

## Next Steps


---

*Source: test_sphere.py:217 | Complexity: Advanced | Last updated: 2026-05-18*