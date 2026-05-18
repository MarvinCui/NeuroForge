# How To: Nifti Labels Masker Create Figure For Report

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Check figure generated in report of NiftiLabelsMasker.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `nilearn.datasets`
- `nilearn.image`
- `nilearn.maskers`
- `nilearn.surface.surface`

**Setup Required:**
```python
# Fixtures: src_masker, mask_img, img
```

## Step-by-Step Guide

### Step 1: 'Check figure generated in report of NiftiLabelsMasker.'

```python
'Check figure generated in report of NiftiLabelsMasker.'
```

### Step 2: Assign positive_img = threshold_img(...)

```python
positive_img = threshold_img(load_sample_motor_activation_image(), 3, cluster_threshold=300, two_sided=False)
```

### Step 3: Assign positive_data = positive_img.get_fdata(...)

```python
positive_data = positive_img.get_fdata()
```

### Step 4: Assign unknown = 1

```python
positive_data[positive_data > 0] = 1
```

### Step 5: Assign positive_img = new_img_like(...)

```python
positive_img = new_img_like(positive_img, data=positive_data)
```

### Step 6: Assign negative_img = threshold_img(...)

```python
negative_img = threshold_img(load_sample_motor_activation_image(), -3, cluster_threshold=100, two_sided=False)
```

### Step 7: Assign negative_data = negative_img.get_fdata(...)

```python
negative_data = negative_img.get_fdata()
```

### Step 8: Assign unknown = 2

```python
negative_data[negative_data < 0] = 2
```

### Step 9: Assign negative_img = new_img_like(...)

```python
negative_img = new_img_like(negative_img, data=negative_data)
```

### Step 10: Assign labels_img = math_img(...)

```python
labels_img = math_img('img1 + img2', img1=positive_img, img2=negative_img)
```

### Step 11: Assign masker = src_masker(...)

```python
masker = src_masker(labels_img, mask_img=mask_img, cmap='RdBu_r')
```

### Step 12: Call masker.fit()

```python
masker.fit(img)
```

### Step 13: Assign labels_image = value

```python
labels_image = masker._reporting_data['labels_image']
```


## Complete Example

```python
# Setup
# Fixtures: src_masker, mask_img, img

# Workflow
'Check figure generated in report of NiftiLabelsMasker.'
positive_img = threshold_img(load_sample_motor_activation_image(), 3, cluster_threshold=300, two_sided=False)
positive_data = positive_img.get_fdata()
positive_data[positive_data > 0] = 1
positive_img = new_img_like(positive_img, data=positive_data)
negative_img = threshold_img(load_sample_motor_activation_image(), -3, cluster_threshold=100, two_sided=False)
negative_data = negative_img.get_fdata()
negative_data[negative_data < 0] = 2
negative_img = new_img_like(negative_img, data=negative_data)
labels_img = math_img('img1 + img2', img1=positive_img, img2=negative_img)
masker = src_masker(labels_img, mask_img=mask_img, cmap='RdBu_r')
masker.fit(img)
labels_image = masker._reporting_data['labels_image']
return masker._create_figure_for_report(labels_image)
```

## Next Steps


---

*Source: test_baseline_comparisons.py:68 | Complexity: Advanced | Last updated: 2026-05-18*