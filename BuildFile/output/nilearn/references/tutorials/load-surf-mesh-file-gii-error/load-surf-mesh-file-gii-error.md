# How To: Load Surf Mesh File Gii Error

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test load surf mesh file gii error

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
# Fixtures: tmp_path, in_memory_mesh
```

## Step-by-Step Guide

### Step 1: Assign coord_array = gifti.GiftiDataArray(...)

```python
coord_array = gifti.GiftiDataArray(data=in_memory_mesh.coordinates, intent=nifti1.intent_codes['NIFTI_INTENT_POINTSET'], datatype='NIFTI_TYPE_FLOAT32')
```

### Step 2: Assign face_array = gifti.GiftiDataArray(...)

```python
face_array = gifti.GiftiDataArray(data=in_memory_mesh.faces, intent=nifti1.intent_codes['NIFTI_INTENT_TRIANGLE'], datatype='NIFTI_TYPE_FLOAT32')
```

### Step 3: Assign filename_gii_mesh_no_point = value

```python
filename_gii_mesh_no_point = tmp_path / 'tmp.gii'
```

### Step 4: Assign gii = gifti.GiftiImage(...)

```python
gii = gifti.GiftiImage(darrays=[face_array, face_array])
```

### Step 5: Call gii.to_filename()

```python
gii.to_filename(filename_gii_mesh_no_point)
```

### Step 6: Assign filename_gii_mesh_no_face = value

```python
filename_gii_mesh_no_face = tmp_path / 'tmp.gii'
```

### Step 7: Assign gii = gifti.GiftiImage(...)

```python
gii = gifti.GiftiImage(darrays=[coord_array, coord_array])
```

### Step 8: Call gii.to_filename()

```python
gii.to_filename(filename_gii_mesh_no_face)
```

### Step 9: Call load_surf_mesh()

```python
load_surf_mesh(filename_gii_mesh_no_point)
```

### Step 10: Call load_surf_mesh()

```python
load_surf_mesh(filename_gii_mesh_no_face)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, in_memory_mesh

# Workflow
coord_array = gifti.GiftiDataArray(data=in_memory_mesh.coordinates, intent=nifti1.intent_codes['NIFTI_INTENT_POINTSET'], datatype='NIFTI_TYPE_FLOAT32')
face_array = gifti.GiftiDataArray(data=in_memory_mesh.faces, intent=nifti1.intent_codes['NIFTI_INTENT_TRIANGLE'], datatype='NIFTI_TYPE_FLOAT32')
filename_gii_mesh_no_point = tmp_path / 'tmp.gii'
gii = gifti.GiftiImage(darrays=[face_array, face_array])
gii.to_filename(filename_gii_mesh_no_point)
with pytest.raises(ValueError, match='NIFTI_INTENT_POINTSET'):
    load_surf_mesh(filename_gii_mesh_no_point)
filename_gii_mesh_no_face = tmp_path / 'tmp.gii'
gii = gifti.GiftiImage(darrays=[coord_array, coord_array])
gii.to_filename(filename_gii_mesh_no_face)
with pytest.raises(ValueError, match='NIFTI_INTENT_TRIANGLE'):
    load_surf_mesh(filename_gii_mesh_no_face)
```

## Next Steps


---

*Source: test_surface.py:312 | Complexity: Advanced | Last updated: 2026-05-18*