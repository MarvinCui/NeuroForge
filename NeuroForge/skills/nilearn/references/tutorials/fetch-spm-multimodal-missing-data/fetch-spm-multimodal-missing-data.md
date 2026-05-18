# How To: Fetch Spm Multimodal Missing Data

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, mock, workflow, integration

## Overview

Workflow: test fetch spm multimodal missing data

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `json`
- `re`
- `shutil`
- `tempfile`
- `uuid`
- `collections`
- `pathlib`
- `numpy`
- `pandas`
- `pytest`
- `nibabel`
- `sklearn.utils`
- `nilearn._utils.data_gen`
- `nilearn._utils.helpers`
- `nilearn.datasets`
- `nilearn.datasets._utils`
- `nilearn.datasets.tests._testing`
- `nilearn.image`

**Setup Required:**
```python
# Fixtures: tmp_path, request_mocker
```

## Step-by-Step Guide

### Step 1: Assign unknown = _generate_spm_multimodal(...)

```python
request_mocker.url_mapping[re.compile('.*multimodal_.*mri.zip')] = _generate_spm_multimodal()
```

**Verification:**
```python
assert (subject_dir / 'fMRI').exists()
```

### Step 2: Assign subject_id = 'sub001'

```python
subject_id = 'sub001'
```

**Verification:**
```python
assert (subject_dir / 'sMRI').exists()
```

### Step 3: Assign subject_dir = value

```python
subject_dir = tmp_path / 'spm_multimodal_fmri' / subject_id
```

**Verification:**
```python
assert isinstance(dataset, Bunch)
```

### Step 4: Assign dataset = func.fetch_spm_multimodal_fmri(...)

```python
dataset = func.fetch_spm_multimodal_fmri(data_dir=tmp_path)
```

**Verification:**
```python
assert isinstance(dataset.anat, str)
```

### Step 5: Call check_type_fetcher()

```python
check_type_fetcher(dataset)
```

**Verification:**
```python
assert isinstance(dataset.func1[0], str)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, request_mocker

# Workflow
request_mocker.url_mapping[re.compile('.*multimodal_.*mri.zip')] = _generate_spm_multimodal()
subject_id = 'sub001'
subject_dir = tmp_path / 'spm_multimodal_fmri' / subject_id
dataset = func.fetch_spm_multimodal_fmri(data_dir=tmp_path)
assert (subject_dir / 'fMRI').exists()
assert (subject_dir / 'sMRI').exists()
assert isinstance(dataset, Bunch)
check_type_fetcher(dataset)
assert isinstance(dataset.anat, str)
assert isinstance(dataset.func1[0], str)
assert len(dataset.func1) == 390
assert isinstance(dataset.func2[0], str)
assert len(dataset.func2) == 390
assert dataset.slice_order == 'descending'
assert isinstance(dataset.trials_ses1, str)
assert isinstance(dataset.trials_ses2, str)
```

## Next Steps


---

*Source: test_func.py:1076 | Complexity: Intermediate | Last updated: 2026-05-18*