# How To: Gifti Img To Mesh

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test gifti img to mesh

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
# Fixtures: in_memory_mesh
```

## Step-by-Step Guide

### Step 1: Assign coord_array = gifti.GiftiDataArray(...)

```python
coord_array = gifti.GiftiDataArray(data=in_memory_mesh.coordinates, datatype='NIFTI_TYPE_FLOAT32')
```

**Verification:**
```python
assert_array_equal(coords, in_memory_mesh.coordinates)
```

### Step 2: Assign coord_array.intent = value

```python
coord_array.intent = nifti1.intent_codes['NIFTI_INTENT_POINTSET']
```

**Verification:**
```python
assert_array_equal(faces, in_memory_mesh.faces)
```

### Step 3: Assign face_array = gifti.GiftiDataArray(...)

```python
face_array = gifti.GiftiDataArray(data=in_memory_mesh.faces, datatype='NIFTI_TYPE_FLOAT32')
```

### Step 4: Assign face_array.intent = value

```python
face_array.intent = nifti1.intent_codes['NIFTI_INTENT_TRIANGLE']
```

### Step 5: Assign gii = gifti.GiftiImage(...)

```python
gii = gifti.GiftiImage(darrays=[coord_array, face_array])
```

### Step 6: Assign unknown = _gifti_img_to_mesh(...)

```python
coords, faces = _gifti_img_to_mesh(gii)
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(coords, in_memory_mesh.coordinates)
```

### Step 8: Call assert_array_equal()

```python
assert_array_equal(faces, in_memory_mesh.faces)
```


## Complete Example

```python
# Setup
# Fixtures: in_memory_mesh

# Workflow
coord_array = gifti.GiftiDataArray(data=in_memory_mesh.coordinates, datatype='NIFTI_TYPE_FLOAT32')
coord_array.intent = nifti1.intent_codes['NIFTI_INTENT_POINTSET']
face_array = gifti.GiftiDataArray(data=in_memory_mesh.faces, datatype='NIFTI_TYPE_FLOAT32')
face_array.intent = nifti1.intent_codes['NIFTI_INTENT_TRIANGLE']
gii = gifti.GiftiImage(darrays=[coord_array, face_array])
coords, faces = _gifti_img_to_mesh(gii)
assert_array_equal(coords, in_memory_mesh.coordinates)
assert_array_equal(faces, in_memory_mesh.faces)
```

## Next Steps


---

*Source: test_surface.py:258 | Complexity: Advanced | Last updated: 2026-05-18*