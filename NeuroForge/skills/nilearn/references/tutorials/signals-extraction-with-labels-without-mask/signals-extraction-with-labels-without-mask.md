# How To: Signals Extraction With Labels Without Mask

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test conversion between signals and images     using regions defined by labels.
    

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
# Fixtures: signals, labels_data, labels_img, shape_3d_default, tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test conversion between signals and images     using regions defined by labels.\n    '

```python
'Test conversion between signals and images     using regions defined by labels.\n    '
```

**Verification:**
```python
assert data_img.shape == (*shape_3d_default, N_TIMEPOINTS)
```

### Step 2: Assign data_img = signals_to_img_labels(...)

```python
data_img = signals_to_img_labels(signals=signals, labels_img=labels_img)
```

**Verification:**
```python
assert np.all(data.std(axis=-1) > 0)
```

### Step 3: Assign data = get_data(...)

```python
data = get_data(data_img)
```

**Verification:**
```python
assert abs(data).max() > 1e-09
```

### Step 4: Call _all_voxel_of_each_region_have_same_values()

```python
_all_voxel_of_each_region_have_same_values(data, labels_data, N_REGIONS, signals)
```

**Verification:**
```python
assert_almost_equal(signals_r, signals)
```

### Step 5: Assign unknown = img_to_signals_labels(...)

```python
signals_r, labels_r, _ = img_to_signals_labels(imgs=data_img, labels_img=labels_img)
```

**Verification:**
```python
assert labels_r == list(range(1, 9))
```

### Step 6: Call assert_almost_equal()

```python
assert_almost_equal(signals_r, signals)
```

**Verification:**
```python
assert_almost_equal(signals_r, signals)
```

### Step 7: Assign filenames = write_imgs_to_path(...)

```python
filenames = write_imgs_to_path(data_img, file_path=tmp_path)
```

**Verification:**
```python
assert labels_r == list(range(1, 9))
```

### Step 8: Assign unknown = img_to_signals_labels(...)

```python
signals_r, labels_r, _ = img_to_signals_labels(imgs=filenames, labels_img=labels_img)
```

### Step 9: Call assert_almost_equal()

```python
assert_almost_equal(signals_r, signals)
```

**Verification:**
```python
assert labels_r == list(range(1, 9))
```


## Complete Example

```python
# Setup
# Fixtures: signals, labels_data, labels_img, shape_3d_default, tmp_path

# Workflow
'Test conversion between signals and images     using regions defined by labels.\n    '
data_img = signals_to_img_labels(signals=signals, labels_img=labels_img)
assert data_img.shape == (*shape_3d_default, N_TIMEPOINTS)
data = get_data(data_img)
assert np.all(data.std(axis=-1) > 0)
assert abs(data).max() > 1e-09
_all_voxel_of_each_region_have_same_values(data, labels_data, N_REGIONS, signals)
signals_r, labels_r, _ = img_to_signals_labels(imgs=data_img, labels_img=labels_img)
assert_almost_equal(signals_r, signals)
assert labels_r == list(range(1, 9))
filenames = write_imgs_to_path(data_img, file_path=tmp_path)
signals_r, labels_r, _ = img_to_signals_labels(imgs=filenames, labels_img=labels_img)
assert_almost_equal(signals_r, signals)
assert labels_r == list(range(1, 9))
```

## Next Steps


---

*Source: test_signal_extraction.py:344 | Complexity: Advanced | Last updated: 2026-05-18*