# How To: Infer Slice Timing Start Time From Dataset

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test inferring slice timing start time from the BIDS dataset.

create_fake_bids_dataset does not add slice timing information
by default so the value returned will be None.

If the metadata is added to the BIDS dataset,
then this value should be returned.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `json`
- `pathlib`
- `pytest`
- `nilearn._utils.data_gen`
- `nilearn.interfaces.bids.query`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test inferring slice timing start time from the BIDS dataset.\n\n    create_fake_bids_dataset does not add slice timing information\n    by default so the value returned will be None.\n\n    If the metadata is added to the BIDS dataset,\n    then this value should be returned.\n    '

```python
'Test inferring slice timing start time from the BIDS dataset.\n\n    create_fake_bids_dataset does not add slice timing information\n    by default so the value returned will be None.\n\n    If the metadata is added to the BIDS dataset,\n    then this value should be returned.\n    '
```

**Verification:**
```python
assert StartTime is expected_StartTime
```

### Step 2: Assign bids_path = create_fake_bids_dataset(...)

```python
bids_path = create_fake_bids_dataset(base_dir=tmp_path, n_sub=1, n_ses=1, tasks=['main'], n_runs=[1])
```

**Verification:**
```python
assert StartTime == expected_StartTime
```

### Step 3: Assign StartTime = infer_slice_timing_start_time_from_dataset(...)

```python
StartTime = infer_slice_timing_start_time_from_dataset(bids_path=tmp_path / bids_path / 'derivatives', filters=[('task', 'main')])
```

### Step 4: Assign expected_StartTime = None

```python
expected_StartTime = None
```

**Verification:**
```python
assert StartTime is expected_StartTime
```

### Step 5: Assign expected_StartTime = 1.0

```python
expected_StartTime = 1.0
```

### Step 6: Call add_metadata_to_bids_dataset()

```python
add_metadata_to_bids_dataset(bids_path=tmp_path / bids_path, metadata={'StartTime': expected_StartTime})
```

### Step 7: Assign StartTime = infer_slice_timing_start_time_from_dataset(...)

```python
StartTime = infer_slice_timing_start_time_from_dataset(bids_path=tmp_path / bids_path / 'derivatives', filters=[('task', 'main')])
```

**Verification:**
```python
assert StartTime == expected_StartTime
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test inferring slice timing start time from the BIDS dataset.\n\n    create_fake_bids_dataset does not add slice timing information\n    by default so the value returned will be None.\n\n    If the metadata is added to the BIDS dataset,\n    then this value should be returned.\n    '
bids_path = create_fake_bids_dataset(base_dir=tmp_path, n_sub=1, n_ses=1, tasks=['main'], n_runs=[1])
StartTime = infer_slice_timing_start_time_from_dataset(bids_path=tmp_path / bids_path / 'derivatives', filters=[('task', 'main')])
expected_StartTime = None
assert StartTime is expected_StartTime
expected_StartTime = 1.0
add_metadata_to_bids_dataset(bids_path=tmp_path / bids_path, metadata={'StartTime': expected_StartTime})
StartTime = infer_slice_timing_start_time_from_dataset(bids_path=tmp_path / bids_path / 'derivatives', filters=[('task', 'main')])
assert StartTime == expected_StartTime
```

## Next Steps


---

*Source: test_query.py:99 | Complexity: Intermediate | Last updated: 2026-05-18*