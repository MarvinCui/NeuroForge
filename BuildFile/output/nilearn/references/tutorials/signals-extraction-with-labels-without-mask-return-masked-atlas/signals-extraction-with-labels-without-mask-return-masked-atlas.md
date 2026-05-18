# How To: Signals Extraction With Labels Without Mask Return Masked Atlas

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test masked_atlas is correct in conversion between signals and images     using regions defined by labels.
    

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `warnings`
- `numpy`
- `pytest`
- `nibabel`
- `numpy.testing`
- `nilearn._utils.data_gen`
- `nilearn._utils.testing`
- `nilearn.conftest`
- `nilearn.exceptions`
- `nilearn.image`
- `nilearn.maskers`
- `nilearn.regions.signal_extraction`

**Setup Required:**
```python
# Fixtures: signals, labels_img
```

## Step-by-Step Guide

### Step 1: 'Test masked_atlas is correct in conversion between signals and images     using regions defined by labels.\n    '

```python
'Test masked_atlas is correct in conversion between signals and images     using regions defined by labels.\n    '
```

**Verification:**
```python
assert_equal(labels_data_r, labels_data)
```

### Step 2: Assign data_img = signals_to_img_labels(...)

```python
data_img = signals_to_img_labels(signals=signals, labels_img=labels_img)
```

**Verification:**
```python
assert list(np.unique(labels_data_r)) == list(range(1, 9))
```

### Step 3: Assign unknown = img_to_signals_labels(...)

```python
_, _, masked_atlas_r = img_to_signals_labels(imgs=data_img, labels_img=labels_img, return_masked_atlas=True)
```

### Step 4: Assign labels_data = get_data(...)

```python
labels_data = get_data(labels_img)
```

### Step 5: Assign labels_data_r = get_data(...)

```python
labels_data_r = get_data(masked_atlas_r)
```

### Step 6: Call assert_equal()

```python
assert_equal(labels_data_r, labels_data)
```

**Verification:**
```python
assert list(np.unique(labels_data_r)) == list(range(1, 9))
```


## Complete Example

```python
# Setup
# Fixtures: signals, labels_img

# Workflow
'Test masked_atlas is correct in conversion between signals and images     using regions defined by labels.\n    '
data_img = signals_to_img_labels(signals=signals, labels_img=labels_img)
_, _, masked_atlas_r = img_to_signals_labels(imgs=data_img, labels_img=labels_img, return_masked_atlas=True)
labels_data = get_data(labels_img)
labels_data_r = get_data(masked_atlas_r)
assert_equal(labels_data_r, labels_data)
assert list(np.unique(labels_data_r)) == list(range(1, 9))
```

## Next Steps


---

*Source: test_signal_extraction.py:381 | Complexity: Intermediate | Last updated: 2026-05-18*