# How To: N Clusters Warning

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test n clusters warning

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `sklearn.utils.estimator_checks`
- `nilearn._utils.data_gen`
- `nilearn._utils.estimator_checks`
- `nilearn._utils.helpers`
- `nilearn._utils.versions`
- `nilearn.maskers`
- `nilearn.regions.hierarchical_kmeans_clustering`
- `nilearn.surface`
- `nilearn.surface.tests.test_surface`

**Setup Required:**
```python
# Fixtures: img_type, rng
```

## Step-by-Step Guide

### Step 1: Assign n_samples = 15

```python
n_samples = 15
```

### Step 2: Assign mesh = value

```python
mesh = {'left': flat_mesh(10, 8), 'right': flat_mesh(9, 7)}
```

### Step 3: Assign data = value

```python
data = {'left': rng.standard_normal(size=(mesh['left'].coordinates.shape[0], n_samples)), 'right': rng.standard_normal(size=(mesh['right'].coordinates.shape[0], n_samples))}
```

### Step 4: Assign img = SurfaceImage(...)

```python
img = SurfaceImage(mesh=mesh, data=data)
```

### Step 5: Assign X = SurfaceMasker.fit_transform(...)

```python
X = SurfaceMasker(standardize=None).fit_transform(img)
```

### Step 6: Assign unknown = generate_fake_fmri(...)

```python
img, _ = generate_fake_fmri(shape=(10, 11, 12), length=n_samples)
```

### Step 7: Assign X = NiftiMasker.fit_transform(...)

```python
X = NiftiMasker(standardize=None).fit_transform(img)
```

### Step 8: Call HierarchicalKMeans.fit_transform()

```python
HierarchicalKMeans(n_clusters=1000).fit_transform(X)
```


## Complete Example

```python
# Setup
# Fixtures: img_type, rng

# Workflow
n_samples = 15
if img_type == 'surface':
    mesh = {'left': flat_mesh(10, 8), 'right': flat_mesh(9, 7)}
    data = {'left': rng.standard_normal(size=(mesh['left'].coordinates.shape[0], n_samples)), 'right': rng.standard_normal(size=(mesh['right'].coordinates.shape[0], n_samples))}
    img = SurfaceImage(mesh=mesh, data=data)
    X = SurfaceMasker(standardize=None).fit_transform(img)
else:
    img, _ = generate_fake_fmri(shape=(10, 11, 12), length=n_samples)
    X = NiftiMasker(standardize=None).fit_transform(img)
with pytest.warns(match='n_clusters should be at most the number of features.'):
    HierarchicalKMeans(n_clusters=1000).fit_transform(X)
```

## Next Steps


---

*Source: test_hierarchical_kmeans_clustering.py:212 | Complexity: Advanced | Last updated: 2026-05-18*