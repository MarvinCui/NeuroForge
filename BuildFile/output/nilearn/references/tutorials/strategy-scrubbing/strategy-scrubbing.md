# How To: Strategy Scrubbing

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Check user specified input for scrubbing strategy.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `re`
- `pandas`
- `pytest`
- `nilearn.interfaces.fmriprep`
- `nilearn.interfaces.fmriprep.load_confounds_strategy`
- `nilearn.interfaces.fmriprep.tests._testing`

**Setup Required:**
```python
# Fixtures: tmp_path, fmriprep_version, volumes_left, len_sample_mask
```

## Step-by-Step Guide

### Step 1: 'Check user specified input for scrubbing strategy.'

```python
'Check user specified input for scrubbing strategy.'
```

**Verification:**
```python
assert len(sample_mask) == volumes_left
```

### Step 2: Assign unknown = create_tmp_filepath(...)

```python
file_nii, _ = create_tmp_filepath(tmp_path, image_type='regular', copy_confounds=True, copy_json=True, fmriprep_version=fmriprep_version)
```

**Verification:**
```python
assert confounds.shape[0] == 30
```

### Step 3: Assign unknown = load_confounds_strategy(...)

```python
confounds, sample_mask = load_confounds_strategy(file_nii, denoise_strategy='scrubbing', fd_threshold=0.15)
```

**Verification:**
```python
assert len(sample_mask) == len_sample_mask
```

### Step 4: Assign unknown = load_confounds_strategy(...)

```python
confounds, sample_mask = load_confounds_strategy(file_nii, denoise_strategy='scrubbing', fd_threshold=1, std_dvars_threshold=5)
```

**Verification:**
```python
assert check in confounds.columns
```

### Step 5: Assign unknown = load_confounds_strategy(...)

```python
confounds, sample_mask = load_confounds_strategy(file_nii, denoise_strategy='scrubbing', global_signal='full')
```

**Verification:**
```python
assert check in confounds.columns
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, fmriprep_version, volumes_left, len_sample_mask

# Workflow
'Check user specified input for scrubbing strategy.'
file_nii, _ = create_tmp_filepath(tmp_path, image_type='regular', copy_confounds=True, copy_json=True, fmriprep_version=fmriprep_version)
confounds, sample_mask = load_confounds_strategy(file_nii, denoise_strategy='scrubbing', fd_threshold=0.15)
assert len(sample_mask) == volumes_left
assert confounds.shape[0] == 30
confounds, sample_mask = load_confounds_strategy(file_nii, denoise_strategy='scrubbing', fd_threshold=1, std_dvars_threshold=5)
assert len(sample_mask) == len_sample_mask
confounds, sample_mask = load_confounds_strategy(file_nii, denoise_strategy='scrubbing', global_signal='full')
for check in ['global_signal', 'global_signal_derivative1', 'global_signal_power2', 'global_signal_derivative1_power2']:
    assert check in confounds.columns
```

## Next Steps


---

*Source: test_load_confounds_strategy.py:106 | Complexity: Intermediate | Last updated: 2026-05-18*