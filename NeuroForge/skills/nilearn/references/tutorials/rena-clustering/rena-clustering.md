# How To: Rena Clustering

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test rena clustering

## Prerequisites

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


## Step-by-Step Guide

### Step 1: Assign unknown = generate_fake_fmri(...)

```python
data_img, mask_img = generate_fake_fmri(shape=(10, 11, 12), length=5)
```

**Verification:**
```python
assert rena.n_clusters_ == 10
```

### Step 2: Assign data = get_data(...)

```python
data = get_data(data_img)
```

**Verification:**
```python
assert X.shape == X_compress.shape
```

### Step 3: Assign mask = get_data(...)

```python
mask = get_data(mask_img)
```

**Verification:**
```python
assert n_clusters != rena.n_clusters_
```

### Step 4: Assign X = np.empty(...)

```python
X = np.empty((data.shape[3], int(mask.sum())))
```

### Step 5: Assign nifti_masker = NiftiMasker.fit(...)

```python
nifti_masker = NiftiMasker(mask_img=mask_img, standardize=None).fit()
```

### Step 6: Assign n_voxels = value

```python
n_voxels = nifti_masker.transform(data_img).shape[1]
```

### Step 7: Assign rena = ReNA(...)

```python
rena = ReNA(mask_img, n_clusters=10)
```

### Step 8: Assign X_red = rena.fit_transform(...)

```python
X_red = rena.fit_transform(X)
```

### Step 9: Assign X_compress = rena.inverse_transform(...)

```python
X_compress = rena.inverse_transform(X_red)
```

**Verification:**
```python
assert rena.n_clusters_ == 10
```

### Step 10: Assign memory = Memory(...)

```python
memory = Memory(location=None)
```

### Step 11: Assign rena = ReNA(...)

```python
rena = ReNA(mask_img, n_clusters=-2, memory=memory)
```

### Step 12: Assign rena = ReNA(...)

```python
rena = ReNA(mask_img, n_clusters=10, scaling=True)
```

### Step 13: Assign X_red = rena.fit_transform(...)

```python
X_red = rena.fit_transform(X)
```

### Step 14: Assign X_compress = rena.inverse_transform(...)

```python
X_compress = rena.inverse_transform(X_red)
```

### Step 15: Assign unknown = value

```python
X[i, :] = np.copy(data[:, :, :, i])[get_data(mask_img) != 0]
```

### Step 16: Call rena.fit()

```python
rena.fit(X)
```

### Step 17: Assign rena = ReNA(...)

```python
rena = ReNA(mask_img, n_iter=n_iter, memory=memory)
```

### Step 18: Assign rena = ReNA.fit(...)

```python
rena = ReNA(mask_img, n_clusters=n_clusters, n_iter=1, memory=memory).fit(X)
```

**Verification:**
```python
assert n_clusters != rena.n_clusters_
```

### Step 19: Call rena.fit()

```python
rena.fit(X)
```


## Complete Example

```python
# Workflow
data_img, mask_img = generate_fake_fmri(shape=(10, 11, 12), length=5)
data = get_data(data_img)
mask = get_data(mask_img)
X = np.empty((data.shape[3], int(mask.sum())))
for i in range(data.shape[3]):
    X[i, :] = np.copy(data[:, :, :, i])[get_data(mask_img) != 0]
nifti_masker = NiftiMasker(mask_img=mask_img, standardize=None).fit()
n_voxels = nifti_masker.transform(data_img).shape[1]
rena = ReNA(mask_img, n_clusters=10)
X_red = rena.fit_transform(X)
X_compress = rena.inverse_transform(X_red)
assert rena.n_clusters_ == 10
assert X.shape == X_compress.shape
memory = Memory(location=None)
rena = ReNA(mask_img, n_clusters=-2, memory=memory)
with pytest.raises(ValueError):
    rena.fit(X)
rena = ReNA(mask_img, n_clusters=10, scaling=True)
X_red = rena.fit_transform(X)
X_compress = rena.inverse_transform(X_red)
for n_iter in [-2, 0]:
    rena = ReNA(mask_img, n_iter=n_iter, memory=memory)
    with pytest.raises(ValueError):
        rena.fit(X)
for n_clusters in [1, 2, 4, 8]:
    rena = ReNA(mask_img, n_clusters=n_clusters, n_iter=1, memory=memory).fit(X)
    assert n_clusters != rena.n_clusters_
del n_voxels, X_red, X_compress
```

## Next Steps


---

*Source: test_rena_clustering.py:86 | Complexity: Advanced | Last updated: 2026-05-18*