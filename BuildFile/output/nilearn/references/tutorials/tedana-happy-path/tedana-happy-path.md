# How To: Tedana Happy Path

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test TEDANA related file input.

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

### Step 1: 'Test TEDANA related file input.'

```python
'Test TEDANA related file input.'
```

**Verification:**
```python
assert conf.size > 0
```

### Step 2: Assign unknown = create_tmp_filepath(...)

```python
tedana_nii, _ = create_tmp_filepath(tmp_path, image_type='tedana', copy_confounds=True)
```

**Verification:**
```python
assert conf.size > 0 and any(('rejected' in col for col in conf.columns))
```

### Step 3: Assign unknown = load_confounds(...)

```python
conf, _ = load_confounds(tedana_nii, strategy=('tedana',))
```

**Verification:**
```python
assert conf.size > 0 and any(('rejected' in col for col in conf.columns)) and any(('accepted' in col for col in conf.columns))
```

### Step 4: Assign unknown = load_confounds(...)

```python
conf, _ = load_confounds(tedana_nii, strategy=('tedana',), tedana='aggressive')
```

**Verification:**
```python
assert conf.size > 0 and any(('rejected' in col for col in conf.columns))
```

### Step 5: Assign unknown = load_confounds(...)

```python
conf, _ = load_confounds(tedana_nii, strategy=('tedana',), tedana='non-aggressive')
```

**Verification:**
```python
assert conf.size > 0 and any(('rejected' in col for col in conf.columns)) and any(('accepted' in col for col in conf.columns))
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test TEDANA related file input.'
tedana_nii, _ = create_tmp_filepath(tmp_path, image_type='tedana', copy_confounds=True)
conf, _ = load_confounds(tedana_nii, strategy=('tedana',))
assert conf.size > 0
conf, _ = load_confounds(tedana_nii, strategy=('tedana',), tedana='aggressive')
assert conf.size > 0 and any(('rejected' in col for col in conf.columns))
conf, _ = load_confounds(tedana_nii, strategy=('tedana',), tedana='non-aggressive')
assert conf.size > 0 and any(('rejected' in col for col in conf.columns)) and any(('accepted' in col for col in conf.columns))
```

## Next Steps


---

*Source: test_load_confounds.py:657 | Complexity: Intermediate | Last updated: 2026-05-18*