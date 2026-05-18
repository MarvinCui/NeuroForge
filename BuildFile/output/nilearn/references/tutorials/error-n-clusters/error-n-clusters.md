# How To: Error N Clusters

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test error n clusters

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
# Fixtures: n_clusters
```

## Step-by-Step Guide

### Step 1: Assign n_samples = 15

```python
n_samples = 15
```

### Step 2: Assign unknown = generate_fake_fmri(...)

```python
data_img, mask_img = generate_fake_fmri(shape=(10, 11, 12), length=n_samples)
```

### Step 3: Assign masker = NiftiMasker.fit(...)

```python
masker = NiftiMasker(mask_img=mask_img, standardize=None).fit()
```

### Step 4: Assign X = masker.transform(...)

```python
X = masker.transform(data_img)
```

### Step 5: Call HierarchicalKMeans.fit()

```python
HierarchicalKMeans(n_clusters=n_clusters).fit(X)
```


## Complete Example

```python
# Setup
# Fixtures: n_clusters

# Workflow
n_samples = 15
data_img, mask_img = generate_fake_fmri(shape=(10, 11, 12), length=n_samples)
masker = NiftiMasker(mask_img=mask_img, standardize=None).fit()
X = masker.transform(data_img)
with pytest.raises(ValueError, match=f'n_clusters should be an integer greater than 0. {n_clusters} was provided.'):
    HierarchicalKMeans(n_clusters=n_clusters).fit(X)
```

## Next Steps


---

*Source: test_hierarchical_kmeans_clustering.py:138 | Complexity: Intermediate | Last updated: 2026-05-18*