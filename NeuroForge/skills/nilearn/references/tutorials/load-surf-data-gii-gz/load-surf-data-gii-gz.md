# How To: Load Surf Data Gii Gz

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test load surf data gii gz

## Prerequisites

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


## Step-by-Step Guide

### Step 1: Assign fsaverage = value

```python
fsaverage = datasets.fetch_surf_fsaverage().sulc_left
```

**Verification:**
```python
assert isinstance(gii, gifti.GiftiImage)
```

### Step 2: Assign gii = _load_surf_files_gifti_gzip(...)

```python
gii = _load_surf_files_gifti_gzip(fsaverage)
```

**Verification:**
```python
assert isinstance(data, np.ndarray)
```

### Step 3: Assign data = load_surf_data(...)

```python
data = load_surf_data(fsaverage)
```

**Verification:**
```python
assert isinstance(gii, gifti.GiftiImage)
```

### Step 4: Assign fsaverage = value

```python
fsaverage = datasets.fetch_surf_fsaverage().pial_left
```

### Step 5: Assign gii = _load_surf_files_gifti_gzip(...)

```python
gii = _load_surf_files_gifti_gzip(fsaverage)
```

**Verification:**
```python
assert isinstance(gii, gifti.GiftiImage)
```


## Complete Example

```python
# Workflow
fsaverage = datasets.fetch_surf_fsaverage().sulc_left
gii = _load_surf_files_gifti_gzip(fsaverage)
assert isinstance(gii, gifti.GiftiImage)
data = load_surf_data(fsaverage)
assert isinstance(data, np.ndarray)
fsaverage = datasets.fetch_surf_fsaverage().pial_left
gii = _load_surf_files_gifti_gzip(fsaverage)
assert isinstance(gii, gifti.GiftiImage)
```

## Next Steps


---

*Source: test_surface.py:160 | Complexity: Intermediate | Last updated: 2026-05-18*