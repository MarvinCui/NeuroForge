# How To: Subject Order With Labels

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Make sure subjects are returned in order.

See https://github.com/nilearn/nilearn/issues/4581

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `shutil`
- `warnings`
- `itertools`
- `pathlib`
- `pandas`
- `pytest`
- `nilearn._utils.data_gen`
- `nilearn.glm.first_level`
- `nilearn.interfaces.bids`
- `nilearn.surface`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Make sure subjects are returned in order.\n\n    See https://github.com/nilearn/nilearn/issues/4581\n    '

```python
'Make sure subjects are returned in order.\n\n    See https://github.com/nilearn/nilearn/issues/4581\n    '
```

**Verification:**
```python
assert returned_subjects == expected_subjects
```

### Step 2: Assign n_sub = 10

```python
n_sub = 10
```

### Step 3: Assign bids_path = create_fake_bids_dataset(...)

```python
bids_path = create_fake_bids_dataset(base_dir=tmp_path, n_sub=n_sub, n_ses=1, tasks=['main'], n_runs=[1])
```

### Step 4: Assign unknown = first_level_from_bids(...)

```python
models, *_ = first_level_from_bids(dataset_path=str(tmp_path / bids_path), sub_labels=['01', '10', '04', '05', '02', '03'], task_label='main', space_label='MNI', img_filters=[('desc', 'preproc')], slice_time_ref=0.0)
```

### Step 5: Assign expected_subjects = value

```python
expected_subjects = ['01', '02', '03', '04', '05', '10']
```

### Step 6: Assign returned_subjects = value

```python
returned_subjects = [model.subject_label for model in models]
```

**Verification:**
```python
assert returned_subjects == expected_subjects
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Make sure subjects are returned in order.\n\n    See https://github.com/nilearn/nilearn/issues/4581\n    '
n_sub = 10
bids_path = create_fake_bids_dataset(base_dir=tmp_path, n_sub=n_sub, n_ses=1, tasks=['main'], n_runs=[1])
models, *_ = first_level_from_bids(dataset_path=str(tmp_path / bids_path), sub_labels=['01', '10', '04', '05', '02', '03'], task_label='main', space_label='MNI', img_filters=[('desc', 'preproc')], slice_time_ref=0.0)
expected_subjects = ['01', '02', '03', '04', '05', '10']
returned_subjects = [model.subject_label for model in models]
assert returned_subjects == expected_subjects
```

## Next Steps


---

*Source: test_first_level_from_bids.py:996 | Complexity: Intermediate | Last updated: 2026-05-18*