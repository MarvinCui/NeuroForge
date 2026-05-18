# How To: Freesurfer Density Operation

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test freesurfer density operation

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `itertools`
- `pathlib`
- `tempfile`
- `urllib.error`
- `nibabel`
- `numpy`
- `numpy.testing`
- `pytest`
- `dipy.data`
- `dipy.io.surface`
- `dipy.io.utils`
- `dipy.utils.optpkg`

**Setup Required:**
```python
# Fixtures: dataset, hemisphere, type
```

## Step-by-Step Guide

### Step 1: Assign prefix = value

```python
prefix = 'baf' if dataset == 'big_affine_freesurfer' else 'saf'
```

**Verification:**
```python
assert sfs.is_bbox_in_vox_valid()
```

### Step 2: Assign fname = value

```python
fname = f'{prefix}_{hemisphere}.{type}'
```

### Step 3: Assign sfs = load_surface(...)

```python
sfs = load_surface(FILEPATH_DIX[fname], FILEPATH_DIX[f'{prefix}_t1.nii.gz'])
```

**Verification:**
```python
assert sfs.is_bbox_in_vox_valid()
```

### Step 4: Assign data = np.zeros(...)

```python
data = np.zeros(sfs.dimensions, dtype=np.uint32)
```

### Step 5: Call sfs.to_vox()

```python
sfs.to_vox()
```

### Step 6: Call sfs.to_corner()

```python
sfs.to_corner()
```

### Step 7: Assign barycenter = np.mean(...)

```python
barycenter = np.mean(np.argwhere(data), axis=0)
```

### Step 8: Call npt.assert_()

```python
npt.assert_(np.linalg.norm(barycenter - approx_barycenter) < 2.0)
```

### Step 9: Assign coord = tuple(...)

```python
coord = tuple(vertex.astype(np.int32))
```

### Step 10: Call nib.save()

```python
nib.save(nib.Nifti1Image(data, sfs.affine), Path(tmpdir) / f'{hemisphere}_{type}.nii.gz')
```

### Step 11: Assign approx_barycenter = value

```python
approx_barycenter = [141, 100, 82] if hemisphere == 'lh' else [80, 101, 83]
```

### Step 12: Assign approx_barycenter = value

```python
approx_barycenter = [139, 96, 80] if hemisphere == 'lh' else [79, 97, 78]
```


## Complete Example

```python
# Setup
# Fixtures: dataset, hemisphere, type

# Workflow
prefix = 'baf' if dataset == 'big_affine_freesurfer' else 'saf'
fname = f'{prefix}_{hemisphere}.{type}'
sfs = load_surface(FILEPATH_DIX[fname], FILEPATH_DIX[f'{prefix}_t1.nii.gz'])
assert sfs.is_bbox_in_vox_valid()
data = np.zeros(sfs.dimensions, dtype=np.uint32)
sfs.to_vox()
sfs.to_corner()
for vertex in sfs.vertices:
    coord = tuple(vertex.astype(np.int32))
    data[coord] += 1
with TemporaryDirectory() as tmpdir:
    nib.save(nib.Nifti1Image(data, sfs.affine), Path(tmpdir) / f'{hemisphere}_{type}.nii.gz')
barycenter = np.mean(np.argwhere(data), axis=0)
if dataset == 'small_affine_freesurfer':
    approx_barycenter = [141, 100, 82] if hemisphere == 'lh' else [80, 101, 83]
elif dataset == 'big_affine_freesurfer':
    approx_barycenter = [139, 96, 80] if hemisphere == 'lh' else [79, 97, 78]
npt.assert_(np.linalg.norm(barycenter - approx_barycenter) < 2.0)
```

## Next Steps


---

*Source: test_surface.py:119 | Complexity: Advanced | Last updated: 2026-05-18*