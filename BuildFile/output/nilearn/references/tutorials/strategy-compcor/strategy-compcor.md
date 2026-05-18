# How To: Strategy Compcor

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Check user specified input for compcor strategy.

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
# Fixtures: tmp_path, fmriprep_version
```

## Step-by-Step Guide

### Step 1: 'Check user specified input for compcor strategy.'

```python
'Check user specified input for compcor strategy.'
```

**Verification:**
```python
assert 't_comp_cor_' not in compcor_col_str_anat
```

### Step 2: Assign unknown = create_tmp_filepath(...)

```python
file_nii, _ = create_tmp_filepath(tmp_path, image_type='regular', copy_confounds=True, copy_json=True, fmriprep_version=fmriprep_version)
```

**Verification:**
```python
assert expected not in compcor_col_str_anat
```

### Step 3: Assign unknown = load_confounds_strategy(...)

```python
confounds, _ = load_confounds_strategy(file_nii, denoise_strategy='compcor')
```

**Verification:**
```python
assert 'global_signal' not in compcor_col_str_anat
```

### Step 4: Assign compcor_col_str_anat = unknown.join(...)

```python
compcor_col_str_anat = ''.join(confounds.columns)
```

**Verification:**
```python
assert 'global_signal' in compcor_col_str_anat
```

### Step 5: Assign expected = value

```python
expected = 'a_comp_cor_57' if fmriprep_version == '1.4.x' else 'w_comp_cor_00'
```

**Verification:**
```python
assert expected not in compcor_col_str_anat
```

### Step 6: Assign unknown = load_confounds_strategy(...)

```python
confounds, _ = load_confounds_strategy(file_nii, denoise_strategy='compcor', global_signal='basic')
```

### Step 7: Assign compcor_col_str_anat = unknown.join(...)

```python
compcor_col_str_anat = ''.join(confounds.columns)
```

**Verification:**
```python
assert 'global_signal' in compcor_col_str_anat
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, fmriprep_version

# Workflow
'Check user specified input for compcor strategy.'
file_nii, _ = create_tmp_filepath(tmp_path, image_type='regular', copy_confounds=True, copy_json=True, fmriprep_version=fmriprep_version)
confounds, _ = load_confounds_strategy(file_nii, denoise_strategy='compcor')
compcor_col_str_anat = ''.join(confounds.columns)
assert 't_comp_cor_' not in compcor_col_str_anat
expected = 'a_comp_cor_57' if fmriprep_version == '1.4.x' else 'w_comp_cor_00'
assert expected not in compcor_col_str_anat
assert 'global_signal' not in compcor_col_str_anat
confounds, _ = load_confounds_strategy(file_nii, denoise_strategy='compcor', global_signal='basic')
compcor_col_str_anat = ''.join(confounds.columns)
assert 'global_signal' in compcor_col_str_anat
```

## Next Steps


---

*Source: test_load_confounds_strategy.py:153 | Complexity: Intermediate | Last updated: 2026-05-18*