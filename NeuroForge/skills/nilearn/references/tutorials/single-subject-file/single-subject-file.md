# How To: Single Subject File

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test with a single-subject dataset with globbing and path.

Only for nifti as we cannot read surface from file.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `sklearn`
- `sklearn.utils.estimator_checks`
- `nilearn._utils.estimator_checks`
- `nilearn._utils.testing`
- `nilearn._utils.versions`
- `nilearn.decomposition`
- `nilearn.decomposition._multi_pca`
- `nilearn.decomposition.tests.conftest`
- `nilearn.maskers`

**Setup Required:**
```python
# Fixtures: data_type, canica_data_single_img, estimator, tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test with a single-subject dataset with globbing and path.\n\n    Only for nifti as we cannot read surface from file.\n    '

```python
'Test with a single-subject dataset with globbing and path.\n\n    Only for nifti as we cannot read surface from file.\n    '
```

### Step 2: Assign est = estimator(...)

```python
est = estimator(n_components=4, random_state=RANDOM_STATE, standardize='zscore_sample')
```

### Step 3: Assign img = write_imgs_to_path(...)

```python
img = write_imgs_to_path(canica_data_single_img, file_path=tmp_path, create_files=True, use_wildcards=True)
```

### Step 4: Call est.fit()

```python
est.fit(img)
```

### Step 5: Call check_decomposition_estimator()

```python
check_decomposition_estimator(est, data_type)
```

### Step 6: Call est.transform()

```python
est.transform(img)
```

### Step 7: Assign est = clone(...)

```python
est = clone(est)
```

### Step 8: Assign tmp_file = value

```python
tmp_file = tmp_path / 'tmp.nii.gz'
```

### Step 9: Call canica_data_single_img.to_filename()

```python
canica_data_single_img.to_filename(tmp_file)
```

### Step 10: Call est.fit()

```python
est.fit(tmp_file)
```

### Step 11: Call check_decomposition_estimator()

```python
check_decomposition_estimator(est, data_type)
```

### Step 12: Call est.transform()

```python
est.transform(tmp_file)
```


## Complete Example

```python
# Setup
# Fixtures: data_type, canica_data_single_img, estimator, tmp_path

# Workflow
'Test with a single-subject dataset with globbing and path.\n\n    Only for nifti as we cannot read surface from file.\n    '
est = estimator(n_components=4, random_state=RANDOM_STATE, standardize='zscore_sample')
img = write_imgs_to_path(canica_data_single_img, file_path=tmp_path, create_files=True, use_wildcards=True)
est.fit(img)
check_decomposition_estimator(est, data_type)
est.transform(img)
est = clone(est)
tmp_file = tmp_path / 'tmp.nii.gz'
canica_data_single_img.to_filename(tmp_file)
est.fit(tmp_file)
check_decomposition_estimator(est, data_type)
est.transform(tmp_file)
```

## Next Steps


---

*Source: test_decomposition_estimators.py:418 | Complexity: Advanced | Last updated: 2026-05-18*