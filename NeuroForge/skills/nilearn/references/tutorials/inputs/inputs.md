# How To: Inputs

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test multiple images as input.

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
# Fixtures: tmp_path, image_type
```

## Step-by-Step Guide

### Step 1: 'Test multiple images as input.'

```python
'Test multiple images as input.'
```

**Verification:**
```python
assert len(conf) == 2
```

### Step 2: Assign files = value

```python
files = []
```

**Verification:**
```python
assert len(conf) == 2
```

### Step 3: Assign unknown = create_tmp_filepath(...)

```python
nii, _ = create_tmp_filepath(tmp_path, bids_fields={'entities': {'sub': f'test{i + 1}', 'ses': 'test', 'task': 'testimg', 'run': '01'}}, image_type=image_type, copy_confounds=True, copy_json=True)
```

### Step 4: Call files.append()

```python
files.append(nii)
```

### Step 5: Assign unknown = load_confounds(...)

```python
conf, _ = load_confounds(files, strategy=('ica_aroma',))
```

### Step 6: Assign unknown = load_confounds(...)

```python
conf, _ = load_confounds(files)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, image_type

# Workflow
'Test multiple images as input.'
files = []
for i in range(2):
    nii, _ = create_tmp_filepath(tmp_path, bids_fields={'entities': {'sub': f'test{i + 1}', 'ses': 'test', 'task': 'testimg', 'run': '01'}}, image_type=image_type, copy_confounds=True, copy_json=True)
    files.append(nii)
if image_type == 'ica_aroma':
    conf, _ = load_confounds(files, strategy=('ica_aroma',))
else:
    conf, _ = load_confounds(files)
assert len(conf) == 2
```

## Next Steps


---

*Source: test_load_confounds.py:788 | Complexity: Intermediate | Last updated: 2026-05-18*