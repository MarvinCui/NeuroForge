# How To: Dict Learning

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Check content of components_img_.

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
# Fixtures: decomposition_mask_img, canica_components, canica_data, data_type
```

## Step-by-Step Guide

### Step 1: 'Check content of components_img_.'

```python
'Check content of components_img_.'
```

**Verification:**
```python
assert recovered_maps >= 2
```

### Step 2: Assign masker = NiftiMasker.fit(...)

```python
masker = NiftiMasker(mask_img=decomposition_mask_img).fit()
```

### Step 3: Assign mask = value

```python
mask = get_data(decomposition_mask_img) != 0
```

### Step 4: Assign flat_mask = mask.ravel(...)

```python
flat_mask = mask.ravel()
```

### Step 5: Assign masked_components = value

```python
masked_components = canica_components[:, flat_mask]
```

### Step 6: Assign dict_init = masker.inverse_transform(...)

```python
dict_init = masker.inverse_transform(masked_components)
```

### Step 7: Assign smoothing_fwhm = None

```python
smoothing_fwhm = None
```

### Step 8: Assign dict_learning = DictLearning(...)

```python
dict_learning = DictLearning(n_components=4, random_state=RANDOM_STATE, dict_init=dict_init, mask=decomposition_mask_img, smoothing_fwhm=smoothing_fwhm, standardize='zscore_sample', alpha=1)
```

### Step 9: Assign dict_learning_auto_init = DictLearning(...)

```python
dict_learning_auto_init = DictLearning(n_components=4, random_state=RANDOM_STATE, mask=decomposition_mask_img, n_epochs=10, smoothing_fwhm=smoothing_fwhm, standardize='zscore_sample', alpha=1)
```

### Step 10: Assign maps = value

```python
maps = {}
```

### Step 11: Call estimator.fit()

```python
estimator.fit(canica_data)
```

### Step 12: Call check_decomposition_estimator()

```python
check_decomposition_estimator(dict_learning, data_type)
```

### Step 13: Assign unknown = get_data(...)

```python
maps[estimator] = get_data(estimator.components_img_)
```

### Step 14: Assign unknown = np.reshape(...)

```python
maps[estimator] = np.reshape(np.rollaxis(maps[estimator], 3, 0)[:, mask], (4, flat_mask.sum()))
```

### Step 15: Assign these_maps = value

```python
these_maps = maps[this_dict_learning]
```

### Step 16: Assign S = np.sqrt(...)

```python
S = np.sqrt(np.sum(masked_components ** 2, axis=1))
```

### Step 17: Assign unknown = 1

```python
S[S == 0] = 1
```

### Step 18: Assign S = np.sqrt(...)

```python
S = np.sqrt(np.sum(these_maps ** 2, axis=1))
```

### Step 19: Assign unknown = 1

```python
S[S == 0] = 1
```

### Step 20: Assign K = np.abs(...)

```python
K = np.abs(masked_components.dot(these_maps.T))
```

### Step 21: Assign recovered_maps = np.sum(...)

```python
recovered_maps = np.sum(K > 0.9)
```

**Verification:**
```python
assert recovered_maps >= 2
```


## Complete Example

```python
# Setup
# Fixtures: decomposition_mask_img, canica_components, canica_data, data_type

# Workflow
'Check content of components_img_.'
masker = NiftiMasker(mask_img=decomposition_mask_img).fit()
mask = get_data(decomposition_mask_img) != 0
flat_mask = mask.ravel()
masked_components = canica_components[:, flat_mask]
dict_init = masker.inverse_transform(masked_components)
smoothing_fwhm = None
dict_learning = DictLearning(n_components=4, random_state=RANDOM_STATE, dict_init=dict_init, mask=decomposition_mask_img, smoothing_fwhm=smoothing_fwhm, standardize='zscore_sample', alpha=1)
dict_learning_auto_init = DictLearning(n_components=4, random_state=RANDOM_STATE, mask=decomposition_mask_img, n_epochs=10, smoothing_fwhm=smoothing_fwhm, standardize='zscore_sample', alpha=1)
maps = {}
for estimator in [dict_learning, dict_learning_auto_init]:
    estimator.fit(canica_data)
    check_decomposition_estimator(dict_learning, data_type)
    maps[estimator] = get_data(estimator.components_img_)
    maps[estimator] = np.reshape(np.rollaxis(maps[estimator], 3, 0)[:, mask], (4, flat_mask.sum()))
for this_dict_learning in [dict_learning]:
    these_maps = maps[this_dict_learning]
    S = np.sqrt(np.sum(masked_components ** 2, axis=1))
    S[S == 0] = 1
    masked_components /= S[:, np.newaxis]
    S = np.sqrt(np.sum(these_maps ** 2, axis=1))
    S[S == 0] = 1
    these_maps /= S[:, np.newaxis]
    K = np.abs(masked_components.dot(these_maps.T))
    recovered_maps = np.sum(K > 0.9)
    assert recovered_maps >= 2
```

## Next Steps


---

*Source: test_dict_learning.py:48 | Complexity: Advanced | Last updated: 2026-05-18*