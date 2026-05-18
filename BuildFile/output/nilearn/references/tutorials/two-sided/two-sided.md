# How To: Two Sided

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test two sided

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
# Fixtures: maps
```

## Step-by-Step Guide

### Step 1: Assign threshold = 0.4

```python
threshold = 0.4
```

**Verification:**
```python
assert not np.array_equal(np.unique(extract_ratio1.regions_img_.get_fdata()), np.unique(extract_ratio2.regions_img_.get_fdata()))
```

### Step 2: Assign thresholding_strategy = 'img_value'

```python
thresholding_strategy = 'img_value'
```

### Step 3: Assign min_region_size = 5

```python
min_region_size = 5
```

### Step 4: Assign extract_ratio1 = RegionExtractor(...)

```python
extract_ratio1 = RegionExtractor(maps, threshold=threshold, thresholding_strategy=thresholding_strategy, two_sided=False, min_region_size=min_region_size, extractor='connected_components')
```

### Step 5: Call extract_ratio1.fit()

```python
extract_ratio1.fit()
```

### Step 6: Assign extract_ratio2 = RegionExtractor(...)

```python
extract_ratio2 = RegionExtractor(maps, threshold=threshold, thresholding_strategy=thresholding_strategy, two_sided=True, min_region_size=min_region_size, extractor='connected_components')
```

### Step 7: Call extract_ratio2.fit()

```python
extract_ratio2.fit()
```

**Verification:**
```python
assert not np.array_equal(np.unique(extract_ratio1.regions_img_.get_fdata()), np.unique(extract_ratio2.regions_img_.get_fdata()))
```


## Complete Example

```python
# Setup
# Fixtures: maps

# Workflow
threshold = 0.4
thresholding_strategy = 'img_value'
min_region_size = 5
extract_ratio1 = RegionExtractor(maps, threshold=threshold, thresholding_strategy=thresholding_strategy, two_sided=False, min_region_size=min_region_size, extractor='connected_components')
extract_ratio1.fit()
extract_ratio2 = RegionExtractor(maps, threshold=threshold, thresholding_strategy=thresholding_strategy, two_sided=True, min_region_size=min_region_size, extractor='connected_components')
extract_ratio2.fit()
assert not np.array_equal(np.unique(extract_ratio1.regions_img_.get_fdata()), np.unique(extract_ratio2.regions_img_.get_fdata()))
```

## Next Steps


---

*Source: test_region_extractor.py:326 | Complexity: Intermediate | Last updated: 2026-05-18*