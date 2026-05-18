# How To: Connected Label Regions Connect Diag False

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test connected label regions connect diag false

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
assert n_labels_wo_connect_diag > n_labels_without_region_extraction
```

### Step 2: Assign n_labels_without_region_extraction = len(...)

```python
n_labels_without_region_extraction = len(np.unique(labels_data))
```

### Step 3: Assign ext_reg_without_connect_diag = connected_label_regions(...)

```python
ext_reg_without_connect_diag = connected_label_regions(img_labels, connect_diag=False)
```

### Step 4: Assign data_wo_connect_diag = get_data(...)

```python
data_wo_connect_diag = get_data(ext_reg_without_connect_diag)
```

### Step 5: Assign n_labels_wo_connect_diag = len(...)

```python
n_labels_wo_connect_diag = len(np.unique(data_wo_connect_diag))
```

**Verification:**
```python
assert n_labels_wo_connect_diag > n_labels_without_region_extraction
```


## Complete Example

```python
# Setup
# Fixtures: img_labels

# Workflow
labels_data = get_data(img_labels)
n_labels_without_region_extraction = len(np.unique(labels_data))
ext_reg_without_connect_diag = connected_label_regions(img_labels, connect_diag=False)
data_wo_connect_diag = get_data(ext_reg_without_connect_diag)
n_labels_wo_connect_diag = len(np.unique(data_wo_connect_diag))
assert n_labels_wo_connect_diag > n_labels_without_region_extraction
```

## Next Steps


---

*Source: test_region_extractor.py:477 | Complexity: Intermediate | Last updated: 2026-05-18*