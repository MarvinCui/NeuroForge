# How To: Strategies

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Check defaults setting of each preset strategy.

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
# Fixtures: tmp_path, denoise_strategy, image_type, fmriprep_version
```

## Step-by-Step Guide

### Step 1: 'Check defaults setting of each preset strategy.'

```python
'Check defaults setting of each preset strategy.'
```

**Verification:**
```python
assert sum(checker) == 1
```

### Step 2: Assign unknown = create_tmp_filepath(...)

```python
file_nii, _ = create_tmp_filepath(tmp_path, image_type=image_type, copy_confounds=True, copy_json=True, fmriprep_version=fmriprep_version)
```

### Step 3: Assign unknown = load_confounds_strategy(...)

```python
confounds, _ = load_confounds_strategy(file_nii, denoise_strategy=denoise_strategy)
```

### Step 4: Assign list_check = _get_headers(...)

```python
list_check = _get_headers(denoise_strategy)
```

### Step 5: Assign checker = value

```python
checker = [re.match(keyword, col) is not None for keyword in list_check]
```

**Verification:**
```python
assert sum(checker) == 1
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, denoise_strategy, image_type, fmriprep_version

# Workflow
'Check defaults setting of each preset strategy.'
file_nii, _ = create_tmp_filepath(tmp_path, image_type=image_type, copy_confounds=True, copy_json=True, fmriprep_version=fmriprep_version)
confounds, _ = load_confounds_strategy(file_nii, denoise_strategy=denoise_strategy)
list_check = _get_headers(denoise_strategy)
for col in confounds.columns:
    checker = [re.match(keyword, col) is not None for keyword in list_check]
    assert sum(checker) == 1
```

## Next Steps


---

*Source: test_load_confounds_strategy.py:52 | Complexity: Intermediate | Last updated: 2026-05-18*