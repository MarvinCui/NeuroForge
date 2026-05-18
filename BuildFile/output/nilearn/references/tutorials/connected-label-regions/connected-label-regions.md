# How To: Connected Label Regions

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test connected label regions

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
# Fixtures: img_labels
```

## Step-by-Step Guide

### Step 1: Assign labels_data = get_data(...)

```python
labels_data = get_data(img_labels)
```

**Verification:**
```python
assert n_labels_without_region_extraction < n_labels_without_min
```

### Step 2: Assign n_labels_without_region_extraction = len(...)

```python
n_labels_without_region_extraction = len(np.unique(labels_data))
```

**Verification:**
```python
assert n_labels_without_min > n_labels_with_min
```

### Step 3: Assign extracted_regions_on_labels_img = connected_label_regions(...)

```python
extracted_regions_on_labels_img = connected_label_regions(img_labels)
```

### Step 4: Assign extracted_regions_labels_data = get_data(...)

```python
extracted_regions_labels_data = get_data(extracted_regions_on_labels_img)
```

### Step 5: Assign n_labels_without_min = len(...)

```python
n_labels_without_min = len(np.unique(extracted_regions_labels_data))
```

**Verification:**
```python
assert n_labels_without_region_extraction < n_labels_without_min
```

### Step 6: Assign extracted_regions_with_min = connected_label_regions(...)

```python
extracted_regions_with_min = connected_label_regions(img_labels, min_size=100)
```

### Step 7: Assign extracted_regions_with_min_data = get_data(...)

```python
extracted_regions_with_min_data = get_data(extracted_regions_with_min)
```

### Step 8: Assign n_labels_with_min = len(...)

```python
n_labels_with_min = len(np.unique(extracted_regions_with_min_data))
```

**Verification:**
```python
assert n_labels_without_min > n_labels_with_min
```


## Complete Example

```python
# Setup
# Fixtures: img_labels

# Workflow
labels_data = get_data(img_labels)
n_labels_without_region_extraction = len(np.unique(labels_data))
extracted_regions_on_labels_img = connected_label_regions(img_labels)
extracted_regions_labels_data = get_data(extracted_regions_on_labels_img)
n_labels_without_min = len(np.unique(extracted_regions_labels_data))
assert n_labels_without_region_extraction < n_labels_without_min
extracted_regions_with_min = connected_label_regions(img_labels, min_size=100)
extracted_regions_with_min_data = get_data(extracted_regions_with_min)
n_labels_with_min = len(np.unique(extracted_regions_with_min_data))
assert n_labels_without_min > n_labels_with_min
```

## Next Steps


---

*Source: test_region_extractor.py:455 | Complexity: Advanced | Last updated: 2026-05-18*