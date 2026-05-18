# How To: Strategy Percentile

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test strategy percentile

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `nibabel`
- `scipy.ndimage`
- `nilearn._utils.data_gen`
- `nilearn._utils.estimator_checks`
- `nilearn._utils.versions`
- `nilearn.conftest`
- `nilearn.exceptions`
- `nilearn.image`
- `nilearn.regions`
- `nilearn.regions.region_extractor`
- `sklearn.utils.estimator_checks`
- `nilearn._utils.estimator_checks`

**Setup Required:**
```python
# Fixtures: maps_and_mask
```

## Step-by-Step Guide

### Step 1: Assign unknown = maps_and_mask

```python
maps, mask_img = maps_and_mask
```

**Verification:**
```python
assert extractor.index_, np.ndarray
```

### Step 2: Assign extractor = RegionExtractor(...)

```python
extractor = RegionExtractor(maps, threshold=30, thresholding_strategy='percentile', mask_img=mask_img, two_sided=True, standardize=None)
```

**Verification:**
```python
assert extractor.regions_img_ != ''
```

### Step 3: Call extractor.fit()

```python
extractor.fit()
```

**Verification:**
```python
assert extractor.regions_img_.shape[-1] >= N_REGIONS
```

### Step 4: Assign n_regions_extracted = value

```python
n_regions_extracted = extractor.regions_img_.shape[-1]
```

**Verification:**
```python
assert expected_signal_shape == signal.shape
```

### Step 5: Assign shape = value

```python
shape = (91, 109, 91, 7)
```

### Step 6: Assign expected_signal_shape = value

```python
expected_signal_shape = (7, n_regions_extracted)
```

### Step 7: Assign n_subjects = 3

```python
n_subjects = 3
```

### Step 8: Assign signal = extractor.transform(...)

```python
signal = extractor.transform(_img_4d_zeros(shape=shape))
```

**Verification:**
```python
assert expected_signal_shape == signal.shape
```


## Complete Example

```python
# Setup
# Fixtures: maps_and_mask

# Workflow
maps, mask_img = maps_and_mask
extractor = RegionExtractor(maps, threshold=30, thresholding_strategy='percentile', mask_img=mask_img, two_sided=True, standardize=None)
extractor.fit()
assert extractor.index_, np.ndarray
assert extractor.regions_img_ != ''
assert extractor.regions_img_.shape[-1] >= N_REGIONS
n_regions_extracted = extractor.regions_img_.shape[-1]
shape = (91, 109, 91, 7)
expected_signal_shape = (7, n_regions_extracted)
n_subjects = 3
for _ in range(n_subjects):
    signal = extractor.transform(_img_4d_zeros(shape=shape))
    assert expected_signal_shape == signal.shape
```

## Next Steps


---

*Source: test_region_extractor.py:359 | Complexity: Advanced | Last updated: 2026-05-18*