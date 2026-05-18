# How To: Surface

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test finding and loading Surface data in BIDS dataset.

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

### Step 1: 'Test finding and loading Surface data in BIDS dataset.'

```python
'Test finding and loading Surface data in BIDS dataset.'
```

### Step 2: Assign n_sub = 2

```python
n_sub = 2
```

### Step 3: Assign tasks = value

```python
tasks = ['main']
```

### Step 4: Assign n_runs = value

```python
n_runs = [2]
```

### Step 5: Assign bids_path = create_fake_bids_dataset(...)

```python
bids_path = create_fake_bids_dataset(base_dir=tmp_path, n_sub=n_sub, n_ses=0, tasks=tasks, n_runs=n_runs, n_vertices=10242)
```

### Step 6: Assign unknown = first_level_from_bids(...)

```python
models, imgs, events, confounds = first_level_from_bids(dataset_path=bids_path, task_label='main', space_label='fsaverage5')
```

### Step 7: Call _check_output_first_level_from_bids()

```python
_check_output_first_level_from_bids(n_sub, models, imgs, events, confounds)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test finding and loading Surface data in BIDS dataset.'
n_sub = 2
tasks = ['main']
n_runs = [2]
bids_path = create_fake_bids_dataset(base_dir=tmp_path, n_sub=n_sub, n_ses=0, tasks=tasks, n_runs=n_runs, n_vertices=10242)
models, imgs, events, confounds = first_level_from_bids(dataset_path=bids_path, task_label='main', space_label='fsaverage5')
_check_output_first_level_from_bids(n_sub, models, imgs, events, confounds)
```

## Next Steps


---

*Source: test_first_level_from_bids.py:1021 | Complexity: Intermediate | Last updated: 2026-05-18*