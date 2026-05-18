# How To: Ica Aroma

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test ICA AROMA related file input.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `re`
- `numpy`
- `pandas`
- `pytest`
- `nibabel`
- `scipy.stats`
- `sklearn.preprocessing`
- `nilearn._utils.data_gen`
- `nilearn._utils.fmriprep_confounds`
- `nilearn.conftest`
- `nilearn.interfaces.bids`
- `nilearn.interfaces.fmriprep`
- `nilearn.interfaces.fmriprep.load_confounds`
- `nilearn.interfaces.fmriprep.tests._testing`
- `nilearn.maskers`
- `nilearn.tests.test_signal`
- `inspect`

**Setup Required:**
```python
# Fixtures: tmp_path, fmriprep_version
```

## Step-by-Step Guide

### Step 1: 'Test ICA AROMA related file input.'

```python
'Test ICA AROMA related file input.'
```

**Verification:**
```python
assert re.match('(?:aroma_motion_+|non_steady_state+)', col_name)
```

### Step 2: Assign unknown = create_tmp_filepath(...)

```python
aroma_nii, _ = create_tmp_filepath(tmp_path, image_type='ica_aroma', copy_confounds=True, fmriprep_version=fmriprep_version)
```

**Verification:**
```python
assert conf.size == 0
```

### Step 3: Assign unknown = create_tmp_filepath(...)

```python
regular_nii, _ = create_tmp_filepath(tmp_path, image_type='regular', copy_confounds=True, fmriprep_version=fmriprep_version)
```

### Step 4: Assign unknown = load_confounds(...)

```python
conf, _ = load_confounds(regular_nii, strategy=('ica_aroma',), ica_aroma='basic')
```

### Step 5: Assign unknown = load_confounds(...)

```python
conf, _ = load_confounds(aroma_nii, strategy=('ica_aroma',), ica_aroma='full')
```

**Verification:**
```python
assert conf.size == 0
```

### Step 6: Assign unknown = load_confounds(...)

```python
conf, _ = load_confounds(regular_nii, strategy=('ica_aroma',), ica_aroma='invalid')
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, fmriprep_version

# Workflow
'Test ICA AROMA related file input.'
aroma_nii, _ = create_tmp_filepath(tmp_path, image_type='ica_aroma', copy_confounds=True, fmriprep_version=fmriprep_version)
regular_nii, _ = create_tmp_filepath(tmp_path, image_type='regular', copy_confounds=True, fmriprep_version=fmriprep_version)
conf, _ = load_confounds(regular_nii, strategy=('ica_aroma',), ica_aroma='basic')
for col_name in conf.columns:
    assert re.match('(?:aroma_motion_+|non_steady_state+)', col_name)
conf, _ = load_confounds(aroma_nii, strategy=('ica_aroma',), ica_aroma='full')
assert conf.size == 0
with pytest.raises(ValueError, match="'ica_aroma' must be one of"):
    conf, _ = load_confounds(regular_nii, strategy=('ica_aroma',), ica_aroma='invalid')
```

## Next Steps


---

*Source: test_load_confounds.py:622 | Complexity: Intermediate | Last updated: 2026-05-18*