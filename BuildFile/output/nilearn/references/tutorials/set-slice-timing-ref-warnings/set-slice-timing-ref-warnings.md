# How To: Set Slice Timing Ref Warnings

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Check that a warning is raised when slice_time_ref is not provided     and cannot be inferred from the dataset.

In this case the model should be created with a slice_time_ref of 0.0.

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

### Step 1: 'Check that a warning is raised when slice_time_ref is not provided     and cannot be inferred from the dataset.\n\n    In this case the model should be created with a slice_time_ref of 0.0.\n    '

```python
'Check that a warning is raised when slice_time_ref is not provided     and cannot be inferred from the dataset.\n\n    In this case the model should be created with a slice_time_ref of 0.0.\n    '
```

**Verification:**
```python
assert models[0].slice_time_ref == expected_slice_time_ref
```

### Step 2: Assign bids_path = create_fake_bids_dataset(...)

```python
bids_path = create_fake_bids_dataset(base_dir=tmp_path, n_sub=10, n_ses=1, tasks=['main'], n_runs=[1])
```

### Step 3: Assign slice_time_ref = None

```python
slice_time_ref = None
```

### Step 4: Assign warning_msg = 'not provided and cannot be inferred'

```python
warning_msg = 'not provided and cannot be inferred'
```

### Step 5: Assign unknown = first_level_from_bids(...)

```python
models, *_ = first_level_from_bids(dataset_path=str(tmp_path / bids_path), task_label='main', space_label='MNI', img_filters=[('desc', 'preproc')], slice_time_ref=slice_time_ref)
```

### Step 6: Assign expected_slice_time_ref = 0.0

```python
expected_slice_time_ref = 0.0
```

**Verification:**
```python
assert models[0].slice_time_ref == expected_slice_time_ref
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Check that a warning is raised when slice_time_ref is not provided     and cannot be inferred from the dataset.\n\n    In this case the model should be created with a slice_time_ref of 0.0.\n    '
bids_path = create_fake_bids_dataset(base_dir=tmp_path, n_sub=10, n_ses=1, tasks=['main'], n_runs=[1])
slice_time_ref = None
warning_msg = 'not provided and cannot be inferred'
with pytest.warns(UserWarning, match=warning_msg):
    models, *_ = first_level_from_bids(dataset_path=str(tmp_path / bids_path), task_label='main', space_label='MNI', img_filters=[('desc', 'preproc')], slice_time_ref=slice_time_ref)
    expected_slice_time_ref = 0.0
    assert models[0].slice_time_ref == expected_slice_time_ref
```

## Next Steps


---

*Source: test_first_level_from_bids.py:138 | Complexity: Intermediate | Last updated: 2026-05-18*