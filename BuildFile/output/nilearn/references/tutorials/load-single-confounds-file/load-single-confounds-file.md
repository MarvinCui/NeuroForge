# How To: Load Single Confounds File

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Check that the load_confounds function returns the same confounds     as _load_single_confounds_file.
    

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

### Step 1: 'Check that the load_confounds function returns the same confounds     as _load_single_confounds_file.\n    '

```python
'Check that the load_confounds function returns the same confounds     as _load_single_confounds_file.\n    '
```

### Step 2: Assign unknown = create_tmp_filepath(...)

```python
nii_file, confounds_file = create_tmp_filepath(tmp_path, copy_confounds=True, fmriprep_version=fmriprep_version)
```

### Step 3: Assign _defaults = value

```python
_defaults = {key: value.default for key, value in inspect.signature(load_confounds).parameters.items()}
```

### Step 4: Call _defaults.pop()

```python
_defaults.pop('img_files')
```

### Step 5: Assign _default_strategy = _defaults.pop(...)

```python
_default_strategy = _defaults.pop('strategy')
```

### Step 6: Assign unknown = _load_single_confounds_file(...)

```python
_, confounds = _load_single_confounds_file(str(confounds_file), strategy=_default_strategy, **_defaults)
```

### Step 7: Assign unknown = load_confounds(...)

```python
confounds_nii, _ = load_confounds(nii_file, strategy=_default_strategy, **_defaults)
```

### Step 8: Call pd.testing.assert_frame_equal()

```python
pd.testing.assert_frame_equal(confounds, confounds_nii)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, fmriprep_version

# Workflow
'Check that the load_confounds function returns the same confounds     as _load_single_confounds_file.\n    '
nii_file, confounds_file = create_tmp_filepath(tmp_path, copy_confounds=True, fmriprep_version=fmriprep_version)
import inspect
_defaults = {key: value.default for key, value in inspect.signature(load_confounds).parameters.items()}
_defaults.pop('img_files')
_default_strategy = _defaults.pop('strategy')
_, confounds = _load_single_confounds_file(str(confounds_file), strategy=_default_strategy, **_defaults)
confounds_nii, _ = load_confounds(nii_file, strategy=_default_strategy, **_defaults)
pd.testing.assert_frame_equal(confounds, confounds_nii)
```

## Next Steps


---

*Source: test_load_confounds.py:309 | Complexity: Advanced | Last updated: 2026-05-18*