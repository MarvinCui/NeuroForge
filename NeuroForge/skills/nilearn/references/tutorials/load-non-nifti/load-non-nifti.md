# How To: Load Non Nifti

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test non-nifti and invalid file type as input.

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
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test non-nifti and invalid file type as input.'

```python
'Test non-nifti and invalid file type as input.'
```

**Verification:**
```python
assert conf.size != 0
```

### Step 2: Assign unknown = create_tmp_filepath(...)

```python
_, tsv = create_tmp_filepath(tmp_path, copy_confounds=True, copy_json=True)
```

**Verification:**
```python
assert conf.size != 0
```

### Step 3: Assign unknown = create_tmp_filepath(...)

```python
cifti, _ = create_tmp_filepath(tmp_path, image_type='cifti', copy_confounds=True, copy_json=True)
```

### Step 4: Assign unknown = load_confounds(...)

```python
conf, _ = load_confounds(cifti)
```

**Verification:**
```python
assert conf.size != 0
```

### Step 5: Assign unknown = create_tmp_filepath(...)

```python
gifti, _ = create_tmp_filepath(tmp_path, image_type='gifti', copy_confounds=True, copy_json=True)
```

### Step 6: Assign unknown = load_confounds(...)

```python
conf, _ = load_confounds(gifti)
```

**Verification:**
```python
assert conf.size != 0
```

### Step 7: Call load_confounds()

```python
load_confounds(str(tsv))
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test non-nifti and invalid file type as input.'
_, tsv = create_tmp_filepath(tmp_path, copy_confounds=True, copy_json=True)
with pytest.raises(ValueError):
    load_confounds(str(tsv))
cifti, _ = create_tmp_filepath(tmp_path, image_type='cifti', copy_confounds=True, copy_json=True)
conf, _ = load_confounds(cifti)
assert conf.size != 0
gifti, _ = create_tmp_filepath(tmp_path, image_type='gifti', copy_confounds=True, copy_json=True)
conf, _ = load_confounds(gifti)
assert conf.size != 0
```

## Next Steps


---

*Source: test_load_confounds.py:555 | Complexity: Intermediate | Last updated: 2026-05-18*