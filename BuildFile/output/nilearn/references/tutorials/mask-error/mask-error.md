# How To: Mask Error

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Check an error is raised if invalid mask is provided before fit.

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

### Step 1: 'Check an error is raised if invalid mask is provided before fit.'

```python
'Check an error is raised if invalid mask is provided before fit.'
```

### Step 2: Assign unknown = generate_fake_fmri(...)

```python
data_img, mask_img = generate_fake_fmri(shape=_shape_3d_default(), length=5)
```

### Step 3: Assign rena = ReNA(...)

```python
rena = ReNA(n_clusters=10, mask_img=1)
```

### Step 4: Assign data = get_data(...)

```python
data = get_data(data_img)
```

### Step 5: Assign mask = get_data(...)

```python
mask = get_data(mask_img)
```

### Step 6: Assign X = np.empty(...)

```python
X = np.empty((data.shape[3], int(mask.sum())))
```

### Step 7: Assign unknown = value

```python
X[i, :] = np.copy(data[:, :, :, i])[get_data(mask_img) != 0]
```

### Step 8: Call rena.fit_transform()

```python
rena.fit_transform(X)
```


## Complete Example

```python
# Workflow
'Check an error is raised if invalid mask is provided before fit.'
data_img, mask_img = generate_fake_fmri(shape=_shape_3d_default(), length=5)
rena = ReNA(n_clusters=10, mask_img=1)
data = get_data(data_img)
mask = get_data(mask_img)
X = np.empty((data.shape[3], int(mask.sum())))
for i in range(data.shape[3]):
    X[i, :] = np.copy(data[:, :, :, i])[get_data(mask_img) != 0]
with pytest.raises(TypeError, match='The mask image should be a'):
    rena.fit_transform(X)
```

## Next Steps


---

*Source: test_rena_clustering.py:68 | Complexity: Advanced | Last updated: 2026-05-18*