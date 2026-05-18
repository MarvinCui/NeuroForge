# How To: Scaling

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test scaling

## Prerequisites

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


## Step-by-Step Guide

### Step 1: Assign n_samples = 15

```python
n_samples = 15
```

**Verification:**
```python
assert_array_almost_equal(np.asarray([np.sqrt(s) * a for s, a in zip(sizes, X_red.T, strict=False)]).T, X_red_scaled)
```

### Step 2: Assign n_clusters = 8

```python
n_clusters = 8
```

**Verification:**
```python
assert_array_almost_equal(X_compress, X_compress_scaled)
```

### Step 3: Assign unknown = generate_fake_fmri(...)

```python
data_img, mask_img = generate_fake_fmri(shape=(10, 11, 12), length=n_samples)
```

### Step 4: Assign masker = NiftiMasker.fit(...)

```python
masker = NiftiMasker(mask_img=mask_img, standardize=None).fit()
```

### Step 5: Assign X = masker.transform(...)

```python
X = masker.transform(data_img)
```

### Step 6: Assign hkmeans = HierarchicalKMeans(...)

```python
hkmeans = HierarchicalKMeans(n_clusters=n_clusters)
```

### Step 7: Assign X_red = hkmeans.fit_transform(...)

```python
X_red = hkmeans.fit_transform(X)
```

### Step 8: Assign X_compress = hkmeans.inverse_transform(...)

```python
X_compress = hkmeans.inverse_transform(X_red)
```

### Step 9: Assign hkmeans_scaled = HierarchicalKMeans(...)

```python
hkmeans_scaled = HierarchicalKMeans(n_clusters=n_clusters, scaling=True)
```

### Step 10: Assign X_red_scaled = hkmeans_scaled.fit_transform(...)

```python
X_red_scaled = hkmeans_scaled.fit_transform(X)
```

### Step 11: Assign sizes = value

```python
sizes = hkmeans_scaled.sizes_
```

### Step 12: Assign X_compress_scaled = hkmeans_scaled.inverse_transform(...)

```python
X_compress_scaled = hkmeans_scaled.inverse_transform(X_red_scaled)
```

### Step 13: Call assert_array_almost_equal()

```python
assert_array_almost_equal(np.asarray([np.sqrt(s) * a for s, a in zip(sizes, X_red.T, strict=False)]).T, X_red_scaled)
```

### Step 14: Call assert_array_almost_equal()

```python
assert_array_almost_equal(X_compress, X_compress_scaled)
```


## Complete Example

```python
# Workflow
n_samples = 15
n_clusters = 8
data_img, mask_img = generate_fake_fmri(shape=(10, 11, 12), length=n_samples)
masker = NiftiMasker(mask_img=mask_img, standardize=None).fit()
X = masker.transform(data_img)
hkmeans = HierarchicalKMeans(n_clusters=n_clusters)
X_red = hkmeans.fit_transform(X)
X_compress = hkmeans.inverse_transform(X_red)
hkmeans_scaled = HierarchicalKMeans(n_clusters=n_clusters, scaling=True)
X_red_scaled = hkmeans_scaled.fit_transform(X)
sizes = hkmeans_scaled.sizes_
X_compress_scaled = hkmeans_scaled.inverse_transform(X_red_scaled)
assert_array_almost_equal(np.asarray([np.sqrt(s) * a for s, a in zip(sizes, X_red.T, strict=False)]).T, X_red_scaled)
assert_array_almost_equal(X_compress, X_compress_scaled)
```

## Next Steps


---

*Source: test_hierarchical_kmeans_clustering.py:155 | Complexity: Advanced | Last updated: 2026-05-18*