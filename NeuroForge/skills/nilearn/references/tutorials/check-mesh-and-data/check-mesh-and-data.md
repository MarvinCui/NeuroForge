# How To: Check Mesh And Data

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test check mesh and data

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `warnings`
- `pathlib`
- `numpy`
- `pytest`
- `nibabel`
- `numpy.testing`
- `scipy.spatial`
- `scipy.stats`
- `sklearn.exceptions`
- `nilearn`
- `nilearn._utils`
- `nilearn._utils.helpers`
- `nilearn.image`
- `nilearn.surface.surface`

**Setup Required:**
```python
# Fixtures: rng, in_memory_mesh
```

## Step-by-Step Guide

### Step 1: Assign data = value

```python
data = in_memory_mesh.coordinates[:, 0]
```

**Verification:**
```python
assert (m[0] == in_memory_mesh.coordinates).all()
```

### Step 2: Assign unknown = check_mesh_and_data(...)

```python
m, d = check_mesh_and_data(in_memory_mesh, data)
```

**Verification:**
```python
assert (m[1] == in_memory_mesh.faces).all()
```

### Step 3: Assign wrong_faces = rng.integers(...)

```python
wrong_faces = rng.integers(in_memory_mesh.n_vertices + 1, size=(30, 3))
```

**Verification:**
```python
assert (d == data).all()
```

### Step 4: Assign data = value

```python
data = in_memory_mesh.coordinates[::2, 0]
```

### Step 5: Call InMemoryMesh()

```python
InMemoryMesh(in_memory_mesh.coordinates, wrong_faces)
```

### Step 6: Call check_mesh_and_data()

```python
check_mesh_and_data(in_memory_mesh, data)
```


## Complete Example

```python
# Setup
# Fixtures: rng, in_memory_mesh

# Workflow
data = in_memory_mesh.coordinates[:, 0]
m, d = check_mesh_and_data(in_memory_mesh, data)
assert (m[0] == in_memory_mesh.coordinates).all()
assert (m[1] == in_memory_mesh.faces).all()
assert (d == data).all()
wrong_faces = rng.integers(in_memory_mesh.n_vertices + 1, size=(30, 3))
with pytest.raises(ValueError, match='Mismatch between .* indices of faces .* number of nodes.'):
    InMemoryMesh(in_memory_mesh.coordinates, wrong_faces)
data = in_memory_mesh.coordinates[::2, 0]
with pytest.raises(ValueError, match='Mismatch between number of nodes in mesh'):
    check_mesh_and_data(in_memory_mesh, data)
```

## Next Steps


---

*Source: test_surface.py:81 | Complexity: Intermediate | Last updated: 2026-05-18*