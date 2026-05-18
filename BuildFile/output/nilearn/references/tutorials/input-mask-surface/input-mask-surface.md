# How To: Input Mask Surface

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test if ReNA clustering works in both cases when mask_img is either a
SurfaceImage or SurfaceMasker.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `joblib`
- `numpy.testing`
- `sklearn.utils.estimator_checks`
- `nilearn._utils.data_gen`
- `nilearn._utils.estimator_checks`
- `nilearn._utils.versions`
- `nilearn.conftest`
- `nilearn.image`
- `nilearn.maskers`
- `nilearn.regions.rena_clustering`
- `nilearn.surface`

**Setup Required:**
```python
# Fixtures: surf_img_2d, surf_mask_dim, surf_mask_1d, surf_mask_2d, mask_as, n_clusters
```

## Step-by-Step Guide

### Step 1: 'Test if ReNA clustering works in both cases when mask_img is either a\n    SurfaceImage or SurfaceMasker.\n    '

```python
'Test if ReNA clustering works in both cases when mask_img is either a\n    SurfaceImage or SurfaceMasker.\n    '
```

**Verification:**
```python
assert X_transformed.shape[1] == n_clusters
```

### Step 2: Assign surf_mask = value

```python
surf_mask = surf_mask_1d if surf_mask_dim == 1 else surf_mask_2d()
```

**Verification:**
```python
assert X_inverse.shape == X.shape
```

### Step 3: Assign masker = SurfaceMasker.fit(...)

```python
masker = SurfaceMasker(surf_mask, standardize=None).fit()
```

### Step 4: Assign X = masker.transform(...)

```python
X = masker.transform(surf_img_2d(50))
```

### Step 5: Assign X_transformed = clustering.fit_transform(...)

```python
X_transformed = clustering.fit_transform(X)
```

### Step 6: Assign X_inverse = clustering.inverse_transform(...)

```python
X_inverse = clustering.inverse_transform(X_transformed)
```

**Verification:**
```python
assert X_transformed.shape[1] == n_clusters
```

### Step 7: Assign clustering = ReNA(...)

```python
clustering = ReNA(mask_img=surf_mask, n_clusters=n_clusters)
```

### Step 8: Assign clustering = ReNA(...)

```python
clustering = ReNA(mask_img=masker, n_clusters=n_clusters)
```


## Complete Example

```python
# Setup
# Fixtures: surf_img_2d, surf_mask_dim, surf_mask_1d, surf_mask_2d, mask_as, n_clusters

# Workflow
'Test if ReNA clustering works in both cases when mask_img is either a\n    SurfaceImage or SurfaceMasker.\n    '
surf_mask = surf_mask_1d if surf_mask_dim == 1 else surf_mask_2d()
masker = SurfaceMasker(surf_mask, standardize=None).fit()
X = masker.transform(surf_img_2d(50))
if mask_as == 'surface_image':
    clustering = ReNA(mask_img=surf_mask, n_clusters=n_clusters)
elif mask_as == 'surface_masker':
    clustering = ReNA(mask_img=masker, n_clusters=n_clusters)
X_transformed = clustering.fit_transform(X)
X_inverse = clustering.inverse_transform(X_transformed)
assert X_transformed.shape[1] == n_clusters
assert X_inverse.shape == X.shape
```

## Next Steps


---

*Source: test_rena_clustering.py:197 | Complexity: Advanced | Last updated: 2026-05-18*