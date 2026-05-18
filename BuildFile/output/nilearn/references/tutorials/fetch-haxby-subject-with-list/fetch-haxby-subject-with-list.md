# How To: Fetch Haxby Subject With List

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: test fetch haxby subject with list

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

### Step 1: Assign subjects = value

```python
subjects = [1, 2, 6]
```

**Verification:**
```python
assert len(haxby.func) == len(subjects)
```

### Step 2: Assign unknown = _make_haxby_subject_data

```python
request_mocker.url_mapping[re.compile('.*(subj\\d).*\\.tar\\.gz')] = _make_haxby_subject_data
```

**Verification:**
```python
assert len(haxby.mask_house_little) == len(subjects)
```

### Step 3: Assign unknown = list_to_archive(...)

```python
request_mocker.url_mapping[re.compile('.*stimuli.*')] = list_to_archive([Path('stimuli', 'README')])
```

**Verification:**
```python
assert len(haxby.anat) == len(subjects)
```

### Step 4: Assign haxby = func.fetch_haxby(...)

```python
haxby = func.fetch_haxby(data_dir=tmp_path, subjects=subjects, fetch_stimuli=True, verbose=0)
```

**Verification:**
```python
assert haxby.anat[2] is None
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, request_mocker

# Workflow
subjects = [1, 2, 6]
request_mocker.url_mapping[re.compile('.*(subj\\d).*\\.tar\\.gz')] = _make_haxby_subject_data
request_mocker.url_mapping[re.compile('.*stimuli.*')] = list_to_archive([Path('stimuli', 'README')])
haxby = func.fetch_haxby(data_dir=tmp_path, subjects=subjects, fetch_stimuli=True, verbose=0)
assert len(haxby.func) == len(subjects)
assert len(haxby.mask_house_little) == len(subjects)
assert len(haxby.anat) == len(subjects)
assert haxby.anat[2] is None
assert isinstance(haxby.mask, str)
assert len(haxby.mask_face) == len(subjects)
assert len(haxby.session_target) == len(subjects)
assert len(haxby.mask_vt) == len(subjects)
assert len(haxby.mask_face_little) == len(subjects)
assert 'stimuli' in haxby
```

## Next Steps


---

*Source: test_func.py:142 | Complexity: Intermediate | Last updated: 2026-05-18*