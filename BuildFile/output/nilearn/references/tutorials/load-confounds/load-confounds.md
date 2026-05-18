# How To: Load Confounds

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that only a subset of confounds can be loaded.

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

### Step 1: 'Test that only a subset of confounds can be loaded.'

```python
'Test that only a subset of confounds can be loaded.'
```

**Verification:**
```python
assert len(confounds[0][0].columns) == 189
```

### Step 2: Assign n_sub = 2

```python
n_sub = 2
```

**Verification:**
```python
assert len(confounds[0][0].columns) == 26
```

### Step 3: Assign bids_path = create_fake_bids_dataset(...)

```python
bids_path = create_fake_bids_dataset(base_dir=tmp_path, n_sub=n_sub, n_ses=2, tasks=['main'], n_runs=[2])
```

**Verification:**
```python
assert all((x in confounds[0][0].columns for x in ['csf', 'white_matter']))
```

### Step 4: Assign unknown = first_level_from_bids(...)

```python
_, _, _, confounds = first_level_from_bids(dataset_path=bids_path, task_label='main', space_label='MNI', img_filters=[('desc', 'preproc')], slice_time_ref=0.0)
```

**Verification:**
```python
assert f'{motion}_{dir}{der}{power}' in confounds[0][0].columns
```

### Step 5: Assign unknown = first_level_from_bids(...)

```python
models, imgs, events, confounds = first_level_from_bids(dataset_path=bids_path, task_label='main', space_label='MNI', img_filters=[('desc', 'preproc')], confounds_strategy=('motion', 'wm_csf'), confounds_motion='full', confounds_wm_csf='basic', slice_time_ref=0.0)
```

### Step 6: Call _check_output_first_level_from_bids()

```python
_check_output_first_level_from_bids(n_sub, models, imgs, events, confounds)
```

**Verification:**
```python
assert len(confounds[0][0].columns) == 26
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test that only a subset of confounds can be loaded.'
n_sub = 2
bids_path = create_fake_bids_dataset(base_dir=tmp_path, n_sub=n_sub, n_ses=2, tasks=['main'], n_runs=[2])
_, _, _, confounds = first_level_from_bids(dataset_path=bids_path, task_label='main', space_label='MNI', img_filters=[('desc', 'preproc')], slice_time_ref=0.0)
assert len(confounds[0][0].columns) == 189
models, imgs, events, confounds = first_level_from_bids(dataset_path=bids_path, task_label='main', space_label='MNI', img_filters=[('desc', 'preproc')], confounds_strategy=('motion', 'wm_csf'), confounds_motion='full', confounds_wm_csf='basic', slice_time_ref=0.0)
_check_output_first_level_from_bids(n_sub, models, imgs, events, confounds)
assert len(confounds[0][0].columns) == 26
assert all((x in confounds[0][0].columns for x in ['csf', 'white_matter']))
for dir, motion, der, power in product(['x', 'y', 'z'], ['rot', 'trans'], ['', '_derivative1'], ['', '_power2']):
    assert f'{motion}_{dir}{der}{power}' in confounds[0][0].columns
```

## Next Steps


---

*Source: test_first_level_from_bids.py:846 | Complexity: Intermediate | Last updated: 2026-05-18*