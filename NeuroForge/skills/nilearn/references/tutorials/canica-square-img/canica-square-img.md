# How To: Canica Square Img

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Check content of components.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `nilearn._utils.helpers`
- `nilearn.decomposition.canica`
- `nilearn.decomposition.tests.conftest`
- `nilearn.image`
- `nilearn.surface.surface`

**Setup Required:**
```python
# Fixtures: decomposition_mask_img, canica_components, canica_data
```

## Step-by-Step Guide

### Step 1: 'Check content of components.'

```python
'Check content of components.'
```

**Verification:**
```python
assert np.sum(K_abs > 0.9) == 4
```

### Step 2: Assign smoothing_fwhm = None

```python
smoothing_fwhm = None
```

**Verification:**
```python
assert_array_almost_equal(K_abs, 0, 1)
```

### Step 3: Assign canica = CanICA(...)

```python
canica = CanICA(n_components=4, random_state=RANDOM_STATE, mask=decomposition_mask_img, smoothing_fwhm=smoothing_fwhm, n_init=50, standardize='zscore_sample')
```

### Step 4: Call canica.fit()

```python
canica.fit(canica_data)
```

### Step 5: Assign maps = get_data(...)

```python
maps = get_data(canica.components_img_)
```

### Step 6: Assign maps = np.rollaxis(...)

```python
maps = np.rollaxis(maps, 3, 0)
```

### Step 7: Assign mask = value

```python
mask = get_data(decomposition_mask_img) != 0
```

### Step 8: Assign K = value

```python
K = np.corrcoef(canica_components[:, mask.ravel()], maps[:, mask])[4:, :4]
```

### Step 9: Assign K_abs = np.abs(...)

```python
K_abs = np.abs(K)
```

**Verification:**
```python
assert np.sum(K_abs > 0.9) == 4
```

### Step 10: Call assert_array_almost_equal()

```python
assert_array_almost_equal(K_abs, 0, 1)
```


## Complete Example

```python
# Setup
# Fixtures: decomposition_mask_img, canica_components, canica_data

# Workflow
'Check content of components.'
smoothing_fwhm = None
canica = CanICA(n_components=4, random_state=RANDOM_STATE, mask=decomposition_mask_img, smoothing_fwhm=smoothing_fwhm, n_init=50, standardize='zscore_sample')
canica.fit(canica_data)
maps = get_data(canica.components_img_)
maps = np.rollaxis(maps, 3, 0)
mask = get_data(decomposition_mask_img) != 0
K = np.corrcoef(canica_components[:, mask.ravel()], maps[:, mask])[4:, :4]
K_abs = np.abs(K)
assert np.sum(K_abs > 0.9) == 4
K_abs[K_abs > 0.9] -= 1
assert_array_almost_equal(K_abs, 0, 1)
```

## Next Steps


---

*Source: test_canica.py:52 | Complexity: Advanced | Last updated: 2026-05-18*