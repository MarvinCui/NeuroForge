# How To: Load Surf Mesh File Gii

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test load surf mesh file gii

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

**Verification:**
```python
assert_array_almost_equal(load_surf_mesh(filename_gii_mesh).coordinates, in_memory_mesh.coordinates)
```

### Step 2: Assign face_array = gifti.GiftiDataArray(...)

```python
face_array = gifti.GiftiDataArray(data=in_memory_mesh.faces, intent=nifti1.intent_codes['NIFTI_INTENT_TRIANGLE'], datatype='NIFTI_TYPE_FLOAT32')
```

**Verification:**
```python
assert_array_almost_equal(load_surf_mesh(filename_gii_mesh).faces, in_memory_mesh.faces)
```

### Step 3: Assign gii = gifti.GiftiImage(...)

```python
gii = gifti.GiftiImage(darrays=[coord_array, face_array])
```

### Step 4: Assign filename_gii_mesh = value

```python
filename_gii_mesh = tmp_path / 'tmp.gii'
```

### Step 5: Call gii.to_filename()

```python
gii.to_filename(filename_gii_mesh)
```

### Step 6: Call assert_array_almost_equal()

```python
assert_array_almost_equal(load_surf_mesh(filename_gii_mesh).coordinates, in_memory_mesh.coordinates)
```

### Step 7: Call assert_array_almost_equal()

```python
assert_array_almost_equal(load_surf_mesh(filename_gii_mesh).faces, in_memory_mesh.faces)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, in_memory_mesh

# Workflow
coord_array = gifti.GiftiDataArray(data=in_memory_mesh.coordinates, intent=nifti1.intent_codes['NIFTI_INTENT_POINTSET'], datatype='NIFTI_TYPE_FLOAT32')
face_array = gifti.GiftiDataArray(data=in_memory_mesh.faces, intent=nifti1.intent_codes['NIFTI_INTENT_TRIANGLE'], datatype='NIFTI_TYPE_FLOAT32')
gii = gifti.GiftiImage(darrays=[coord_array, face_array])
filename_gii_mesh = tmp_path / 'tmp.gii'
gii.to_filename(filename_gii_mesh)
assert_array_almost_equal(load_surf_mesh(filename_gii_mesh).coordinates, in_memory_mesh.coordinates)
assert_array_almost_equal(load_surf_mesh(filename_gii_mesh).faces, in_memory_mesh.faces)
```

## Next Steps


---

*Source: test_surface.py:285 | Complexity: Intermediate | Last updated: 2026-05-18*