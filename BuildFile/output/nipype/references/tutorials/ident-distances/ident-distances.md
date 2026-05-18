# How To: Ident Distances

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test ident distances

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pytest`
- `nipype.testing`
- `numpy`
- `nipype.algorithms`
- `interfaces`
- `interfaces.vtkbase`

**Setup Required:**
```python
# Fixtures: tmpdir
```

## Step-by-Step Guide

### Step 1: Call tmpdir.chdir()

```python
tmpdir.chdir()
```

**Verification:**
```python
assert res.outputs.distance == 0.0
```

### Step 2: Assign in_surf = example_data(...)

```python
in_surf = example_data('surf01.vtk')
```

**Verification:**
```python
assert res.outputs.distance == 0.0
```

### Step 3: Assign dist_ident = m.ComputeMeshWarp(...)

```python
dist_ident = m.ComputeMeshWarp()
```

### Step 4: Assign dist_ident.inputs.surface1 = in_surf

```python
dist_ident.inputs.surface1 = in_surf
```

### Step 5: Assign dist_ident.inputs.surface2 = in_surf

```python
dist_ident.inputs.surface2 = in_surf
```

### Step 6: Assign dist_ident.inputs.out_file = value

```python
dist_ident.inputs.out_file = tmpdir.join('distance.npy').strpath
```

### Step 7: Assign res = dist_ident.run(...)

```python
res = dist_ident.run()
```

**Verification:**
```python
assert res.outputs.distance == 0.0
```

### Step 8: Assign dist_ident.inputs.weighting = 'area'

```python
dist_ident.inputs.weighting = 'area'
```

### Step 9: Assign res = dist_ident.run(...)

```python
res = dist_ident.run()
```

**Verification:**
```python
assert res.outputs.distance == 0.0
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir

# Workflow
tmpdir.chdir()
in_surf = example_data('surf01.vtk')
dist_ident = m.ComputeMeshWarp()
dist_ident.inputs.surface1 = in_surf
dist_ident.inputs.surface2 = in_surf
dist_ident.inputs.out_file = tmpdir.join('distance.npy').strpath
res = dist_ident.run()
assert res.outputs.distance == 0.0
dist_ident.inputs.weighting = 'area'
res = dist_ident.run()
assert res.outputs.distance == 0.0
```

## Next Steps


---

*Source: test_mesh_ops.py:13 | Complexity: Advanced | Last updated: 2026-05-18*