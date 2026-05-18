# How To: Connected Label Regions Check Labels String Without List

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: If labels (or names to regions) given is a string without a list     we expect it to be split to regions extracted and returned as list.
    

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
# Fixtures: img_labels, affine_eye, shape_3d_default
```

## Step-by-Step Guide

### Step 1: 'If labels (or names to regions) given is a string without a list     we expect it to be split to regions extracted and returned as list.\n    '

```python
'If labels (or names to regions) given is a string without a list     we expect it to be split to regions extracted and returned as list.\n    '
```

**Verification:**
```python
assert isinstance(new_labels, list)
```

### Step 2: Assign labels_in_str = 'region_a'

```python
labels_in_str = 'region_a'
```

**Verification:**
```python
assert len(new_labels) >= len(combined_labels)
```

### Step 3: Assign labels_img_in_str = generate_labeled_regions(...)

```python
labels_img_in_str = generate_labeled_regions(shape=shape_3d_default, affine=affine_eye, n_regions=1)
```

### Step 4: Assign unknown = connected_label_regions(...)

```python
_, new_labels = connected_label_regions(labels_img_in_str, labels=labels_in_str)
```

**Verification:**
```python
assert isinstance(new_labels, list)
```

### Step 5: Assign combined_labels = value

```python
combined_labels = ['region_a', '1', 'region_b', '2', 'region_c', '3', 'region_d', '4', 'region_e']
```

### Step 6: Assign unknown = connected_label_regions(...)

```python
_, new_labels = connected_label_regions(img_labels, labels=combined_labels)
```

**Verification:**
```python
assert len(new_labels) >= len(combined_labels)
```


## Complete Example

```python
# Setup
# Fixtures: img_labels, affine_eye, shape_3d_default

# Workflow
'If labels (or names to regions) given is a string without a list     we expect it to be split to regions extracted and returned as list.\n    '
labels_in_str = 'region_a'
labels_img_in_str = generate_labeled_regions(shape=shape_3d_default, affine=affine_eye, n_regions=1)
_, new_labels = connected_label_regions(labels_img_in_str, labels=labels_in_str)
assert isinstance(new_labels, list)
combined_labels = ['region_a', '1', 'region_b', '2', 'region_c', '3', 'region_d', '4', 'region_e']
_, new_labels = connected_label_regions(img_labels, labels=combined_labels)
assert len(new_labels) >= len(combined_labels)
```

## Next Steps


---

*Source: test_region_extractor.py:596 | Complexity: Intermediate | Last updated: 2026-05-18*