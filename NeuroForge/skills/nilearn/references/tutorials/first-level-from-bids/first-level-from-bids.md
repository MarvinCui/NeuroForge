# How To: First Level From Bids

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

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
# Fixtures: tmp_path, n_runs, n_ses, task_index, space_label
```

## Step-by-Step Guide

### Step 1: 'Test several BIDS structure.'

```python
'Test several BIDS structure.'
```

**Verification:**
```python
assert len(imgs[0]) == n_imgs_expected
```

### Step 2: Assign n_sub = 2

```python
n_sub = 2
```

### Step 3: Assign tasks = value

```python
tasks = ['localizer', 'main']
```

### Step 4: Assign bids_path = create_fake_bids_dataset(...)

```python
bids_path = create_fake_bids_dataset(base_dir=tmp_path, n_sub=n_sub, n_ses=n_ses, tasks=tasks, n_runs=n_runs)
```

### Step 5: Assign unknown = first_level_from_bids(...)

```python
models, imgs, events, confounds = first_level_from_bids(dataset_path=bids_path, task_label=tasks[task_index], space_label=space_label, img_filters=[('desc', 'preproc')], slice_time_ref=0.0)
```

### Step 6: Call _check_output_first_level_from_bids()

```python
_check_output_first_level_from_bids(n_sub, models, imgs, events, confounds)
```

### Step 7: Assign n_imgs_expected = value

```python
n_imgs_expected = n_ses * n_runs[task_index]
```

### Step 8: Assign no_run_entity = value

```python
no_run_entity = n_runs[task_index] <= 1
```

### Step 9: Assign no_session_level = value

```python
no_session_level = n_ses <= 1
```

**Verification:**
```python
assert len(imgs[0]) == n_imgs_expected
```

### Step 10: Assign n_imgs_expected = value

```python
n_imgs_expected = 1 if no_run_entity else n_runs[task_index]
```

### Step 11: Assign n_imgs_expected = n_ses

```python
n_imgs_expected = n_ses
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, n_runs, n_ses, task_index, space_label

# Workflow
'Test several BIDS structure.'
n_sub = 2
tasks = ['localizer', 'main']
bids_path = create_fake_bids_dataset(base_dir=tmp_path, n_sub=n_sub, n_ses=n_ses, tasks=tasks, n_runs=n_runs)
models, imgs, events, confounds = first_level_from_bids(dataset_path=bids_path, task_label=tasks[task_index], space_label=space_label, img_filters=[('desc', 'preproc')], slice_time_ref=0.0)
_check_output_first_level_from_bids(n_sub, models, imgs, events, confounds)
n_imgs_expected = n_ses * n_runs[task_index]
no_run_entity = n_runs[task_index] <= 1
no_session_level = n_ses <= 1
if no_session_level:
    n_imgs_expected = 1 if no_run_entity else n_runs[task_index]
elif no_run_entity:
    n_imgs_expected = n_ses
assert len(imgs[0]) == n_imgs_expected
```

## Next Steps


---

*Source: test_first_level_from_bids.py:279 | Complexity: Advanced | Last updated: 2026-05-18*