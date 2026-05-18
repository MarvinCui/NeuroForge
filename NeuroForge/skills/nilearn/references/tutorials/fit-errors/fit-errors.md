# How To: Fit Errors

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Fit fail without the proper arguments.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `sklearn`
- `sklearn.utils.estimator_checks`
- `nilearn._utils.estimator_checks`
- `nilearn._utils.testing`
- `nilearn._utils.versions`
- `nilearn.decomposition`
- `nilearn.decomposition._multi_pca`
- `nilearn.decomposition.tests.conftest`
- `nilearn.maskers`

**Setup Required:**
```python
# Fixtures: data_type, decomposition_images, estimator, decomposition_mask_img
```

## Step-by-Step Guide

### Step 1: 'Fit fail without the proper arguments.'

```python
'Fit fail without the proper arguments.'
```

**Verification:**
```python
assert est.masker_.n_elements_ == decomposition_images[0].mesh.n_vertices
```

### Step 2: Assign est = estimator(...)

```python
est = estimator(smoothing_fwhm=None, standardize='zscore_sample')
```

### Step 3: Assign est = estimator(...)

```python
est = estimator(smoothing_fwhm=None, standardize='zscore_sample')
```

### Step 4: Assign est = estimator(...)

```python
est = estimator(n_components=3, mask=decomposition_mask_img, random_state=RANDOM_STATE, smoothing_fwhm=None, standardize='zscore_sample')
```

### Step 5: Assign confounds = value

```python
confounds = [np.arange(N_SAMPLES * 2).reshape(N_SAMPLES, 2)] * len(decomposition_images) * 2
```

### Step 6: Call est.fit()

```python
est.fit([])
```

### Step 7: Call est.fit()

```python
est.fit(decomposition_images, confounds=confounds)
```

### Step 8: Call est.fit()

```python
est.fit(decomposition_images)
```

### Step 9: Call est.fit()

```python
est.fit(decomposition_images)
```

**Verification:**
```python
assert est.masker_.n_elements_ == decomposition_images[0].mesh.n_vertices
```


## Complete Example

```python
# Setup
# Fixtures: data_type, decomposition_images, estimator, decomposition_mask_img

# Workflow
'Fit fail without the proper arguments.'
est = estimator(smoothing_fwhm=None, standardize='zscore_sample')
with pytest.raises(ValueError, match='Need one or more Niimg-like or SurfaceImage objects as input, an empty list was given.'):
    est.fit([])
est = estimator(smoothing_fwhm=None, standardize='zscore_sample')
if data_type == 'nifti':
    with pytest.raises(ValueError, match='The mask is invalid as it is empty'):
        est.fit(decomposition_images)
elif data_type == 'surface':
    est.fit(decomposition_images)
    assert est.masker_.n_elements_ == decomposition_images[0].mesh.n_vertices
est = estimator(n_components=3, mask=decomposition_mask_img, random_state=RANDOM_STATE, smoothing_fwhm=None, standardize='zscore_sample')
confounds = [np.arange(N_SAMPLES * 2).reshape(N_SAMPLES, 2)] * len(decomposition_images) * 2
with pytest.raises(ValueError, match='Number of confounds .* must match number of images .*'):
    est.fit(decomposition_images, confounds=confounds)
```

## Next Steps


---

*Source: test_decomposition_estimators.py:71 | Complexity: Advanced | Last updated: 2026-05-18*