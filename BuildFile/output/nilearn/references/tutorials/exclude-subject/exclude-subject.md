# How To: Exclude Subject

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test several BIDS structure.

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

### Step 1: 'Test several BIDS structure.'

```python
'Test several BIDS structure.'
```

**Verification:**
```python
assert len(models) == 1
```

### Step 2: Assign n_sub = 2

```python
n_sub = 2
```

### Step 3: Assign n_ses = 1

```python
n_ses = 1
```

### Step 4: Assign n_runs = value

```python
n_runs = [1]
```

### Step 5: Assign task_label = 'main'

```python
task_label = 'main'
```

### Step 6: Assign space_label = 'MNI'

```python
space_label = 'MNI'
```

### Step 7: Assign bids_path = create_fake_bids_dataset(...)

```python
bids_path = create_fake_bids_dataset(base_dir=tmp_path, n_sub=n_sub, n_ses=n_ses, tasks=[task_label], n_runs=n_runs)
```

### Step 8: Assign unknown = first_level_from_bids(...)

```python
models, _, _, _ = first_level_from_bids(dataset_path=bids_path, task_label=task_label, space_label=space_label, img_filters=[('desc', 'preproc')], exclude_subjects=['01'], slice_time_ref=0.0)
```

**Verification:**
```python
assert len(models) == 1
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test several BIDS structure.'
n_sub = 2
n_ses = 1
n_runs = [1]
task_label = 'main'
space_label = 'MNI'
bids_path = create_fake_bids_dataset(base_dir=tmp_path, n_sub=n_sub, n_ses=n_ses, tasks=[task_label], n_runs=n_runs)
models, _, _, _ = first_level_from_bids(dataset_path=bids_path, task_label=task_label, space_label=space_label, img_filters=[('desc', 'preproc')], exclude_subjects=['01'], slice_time_ref=0.0)
assert len(models) == 1
```

## Next Steps


---

*Source: test_first_level_from_bids.py:315 | Complexity: Advanced | Last updated: 2026-05-18*