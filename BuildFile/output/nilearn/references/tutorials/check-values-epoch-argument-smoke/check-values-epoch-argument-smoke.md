# How To: Check Values Epoch Argument Smoke

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Smoke test to check different values of the epoch argument.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `nilearn.decomposition.dict_learning`
- `nilearn.decomposition.tests.conftest`
- `nilearn.image`
- `nilearn.maskers`
- `nilearn.surface.surface`

**Setup Required:**
```python
# Fixtures: decomposition_mask_img, n_epochs, canica_components, canica_data, data_type
```

## Step-by-Step Guide

### Step 1: 'Smoke test to check different values of the epoch argument.'

```python
'Smoke test to check different values of the epoch argument.'
```

### Step 2: Assign flat_mask = mask.ravel(...)

```python
flat_mask = mask.ravel()
```

### Step 3: Assign dict_init = masker.inverse_transform(...)

```python
dict_init = masker.inverse_transform(canica_components[:, flat_mask])
```

### Step 4: Assign dict_learning = DictLearning(...)

```python
dict_learning = DictLearning(n_components=4, random_state=RANDOM_STATE, dict_init=dict_init, mask=decomposition_mask_img, n_epochs=n_epochs, smoothing_fwhm=None, standardize='zscore_sample', alpha=1)
```

### Step 5: Call dict_learning.fit()

```python
dict_learning.fit(canica_data)
```

### Step 6: Call check_decomposition_estimator()

```python
check_decomposition_estimator(dict_learning, data_type)
```

### Step 7: Assign masker = NiftiMasker.fit(...)

```python
masker = NiftiMasker(mask_img=decomposition_mask_img).fit()
```

### Step 8: Assign mask = value

```python
mask = get_data(decomposition_mask_img) != 0
```

### Step 9: Assign masker = SurfaceMasker.fit(...)

```python
masker = SurfaceMasker(mask_img=decomposition_mask_img).fit()
```

### Step 10: Assign mask = value

```python
mask = get_surface_data(decomposition_mask_img) != 0
```


## Complete Example

```python
# Setup
# Fixtures: decomposition_mask_img, n_epochs, canica_components, canica_data, data_type

# Workflow
'Smoke test to check different values of the epoch argument.'
if data_type == 'nifti':
    masker = NiftiMasker(mask_img=decomposition_mask_img).fit()
    mask = get_data(decomposition_mask_img) != 0
else:
    masker = SurfaceMasker(mask_img=decomposition_mask_img).fit()
    mask = get_surface_data(decomposition_mask_img) != 0
flat_mask = mask.ravel()
dict_init = masker.inverse_transform(canica_components[:, flat_mask])
dict_learning = DictLearning(n_components=4, random_state=RANDOM_STATE, dict_init=dict_init, mask=decomposition_mask_img, n_epochs=n_epochs, smoothing_fwhm=None, standardize='zscore_sample', alpha=1)
dict_learning.fit(canica_data)
check_decomposition_estimator(dict_learning, data_type)
```

## Next Steps


---

*Source: test_dict_learning.py:17 | Complexity: Advanced | Last updated: 2026-05-18*