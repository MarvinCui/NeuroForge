# How To: Get Metadata From Derivatives

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: No warning should be thrown given derivatives have metadata.

The model created should use the values found in the derivatives.

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

### Step 1: 'No warning should be thrown given derivatives have metadata.\n\n    The model created should use the values found in the derivatives.\n    '

```python
'No warning should be thrown given derivatives have metadata.\n\n    The model created should use the values found in the derivatives.\n    '
```

**Verification:**
```python
assert models[0].t_r == RepetitionTime
```

### Step 2: Assign bids_path = create_fake_bids_dataset(...)

```python
bids_path = create_fake_bids_dataset(base_dir=tmp_path, n_sub=10, n_ses=1, tasks=['main'], n_runs=[1])
```

**Verification:**
```python
assert models[0].slice_time_ref == StartTime / RepetitionTime
```

### Step 3: Assign RepetitionTime = 6.0

```python
RepetitionTime = 6.0
```

### Step 4: Assign StartTime = 2.0

```python
StartTime = 2.0
```

### Step 5: Call add_metadata_to_bids_dataset()

```python
add_metadata_to_bids_dataset(bids_path=tmp_path / bids_path, metadata={'RepetitionTime': RepetitionTime, 'StartTime': StartTime})
```

### Step 6: Call warnings.simplefilter()

```python
warnings.simplefilter('error')
```

### Step 7: Assign unknown = first_level_from_bids(...)

```python
models, *_ = first_level_from_bids(dataset_path=str(tmp_path / bids_path), task_label='main', space_label='MNI', img_filters=[('desc', 'preproc')], slice_time_ref=None)
```

**Verification:**
```python
assert models[0].t_r == RepetitionTime
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'No warning should be thrown given derivatives have metadata.\n\n    The model created should use the values found in the derivatives.\n    '
bids_path = create_fake_bids_dataset(base_dir=tmp_path, n_sub=10, n_ses=1, tasks=['main'], n_runs=[1])
RepetitionTime = 6.0
StartTime = 2.0
add_metadata_to_bids_dataset(bids_path=tmp_path / bids_path, metadata={'RepetitionTime': RepetitionTime, 'StartTime': StartTime})
with warnings.catch_warnings():
    warnings.simplefilter('error')
    models, *_ = first_level_from_bids(dataset_path=str(tmp_path / bids_path), task_label='main', space_label='MNI', img_filters=[('desc', 'preproc')], slice_time_ref=None)
    assert models[0].t_r == RepetitionTime
    assert models[0].slice_time_ref == StartTime / RepetitionTime
```

## Next Steps


---

*Source: test_first_level_from_bids.py:189 | Complexity: Intermediate | Last updated: 2026-05-18*