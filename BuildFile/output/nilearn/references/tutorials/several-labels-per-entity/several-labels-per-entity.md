# How To: Several Labels Per Entity

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Correct files selected when an entity has several possible labels.

Regression test for https://github.com/nilearn/nilearn/issues/3524

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
# Fixtures: tmp_path, entity
```

## Step-by-Step Guide

### Step 1: 'Correct files selected when an entity has several possible labels.\n\n    Regression test for https://github.com/nilearn/nilearn/issues/3524\n    '

```python
'Correct files selected when an entity has several possible labels.\n\n    Regression test for https://github.com/nilearn/nilearn/issues/3524\n    '
```

**Verification:**
```python
assert len(imgs[0]) == n_imgs_expected
```

### Step 2: Assign n_sub = 1

```python
n_sub = 1
```

### Step 3: Assign n_ses = 1

```python
n_ses = 1
```

### Step 4: Assign tasks = value

```python
tasks = ['main']
```

### Step 5: Assign n_runs = value

```python
n_runs = [1]
```

### Step 6: Assign bids_path = create_fake_bids_dataset(...)

```python
bids_path = create_fake_bids_dataset(base_dir=tmp_path, n_sub=n_sub, n_ses=n_ses, tasks=tasks, n_runs=n_runs, entities={entity: ['A', 'B']})
```

### Step 7: Assign unknown = first_level_from_bids(...)

```python
models, imgs, events, confounds = first_level_from_bids(dataset_path=bids_path, task_label='main', space_label='MNI', img_filters=[('desc', 'preproc'), (entity, 'A')], slice_time_ref=0.0)
```

### Step 8: Call _check_output_first_level_from_bids()

```python
_check_output_first_level_from_bids(n_sub, models, imgs, events, confounds)
```

### Step 9: Assign n_imgs_expected = value

```python
n_imgs_expected = n_ses * n_runs[0]
```

**Verification:**
```python
assert len(imgs[0]) == n_imgs_expected
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, entity

# Workflow
'Correct files selected when an entity has several possible labels.\n\n    Regression test for https://github.com/nilearn/nilearn/issues/3524\n    '
n_sub = 1
n_ses = 1
tasks = ['main']
n_runs = [1]
bids_path = create_fake_bids_dataset(base_dir=tmp_path, n_sub=n_sub, n_ses=n_ses, tasks=tasks, n_runs=n_runs, entities={entity: ['A', 'B']})
models, imgs, events, confounds = first_level_from_bids(dataset_path=bids_path, task_label='main', space_label='MNI', img_filters=[('desc', 'preproc'), (entity, 'A')], slice_time_ref=0.0)
_check_output_first_level_from_bids(n_sub, models, imgs, events, confounds)
n_imgs_expected = n_ses * n_runs[0]
assert len(imgs[0]) == n_imgs_expected
```

## Next Steps


---

*Source: test_first_level_from_bids.py:433 | Complexity: Advanced | Last updated: 2026-05-18*