# How To: Infer Repetition Time From Dataset

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test inferring repetition time from the BIDS dataset.

When using create_fake_bids_dataset the value is 1.5 secs by default
in the raw dataset.
When using add_metadata_to_bids_dataset the value is 2.0 secs.

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

### Step 1: 'Test inferring repetition time from the BIDS dataset.\n\n    When using create_fake_bids_dataset the value is 1.5 secs by default\n    in the raw dataset.\n    When using add_metadata_to_bids_dataset the value is 2.0 secs.\n    '

```python
'Test inferring repetition time from the BIDS dataset.\n\n    When using create_fake_bids_dataset the value is 1.5 secs by default\n    in the raw dataset.\n    When using add_metadata_to_bids_dataset the value is 2.0 secs.\n    '
```

**Verification:**
```python
assert t_r == expected_t_r
```

### Step 2: Assign bids_path = create_fake_bids_dataset(...)

```python
bids_path = create_fake_bids_dataset(base_dir=tmp_path, n_sub=1, n_ses=1, tasks=['main'], n_runs=[1])
```

**Verification:**
```python
assert t_r == expected_t_r
```

### Step 3: Assign t_r = infer_repetition_time_from_dataset(...)

```python
t_r = infer_repetition_time_from_dataset(bids_path=tmp_path / bids_path, filters=[('task', 'main')])
```

### Step 4: Assign expected_t_r = 1.5

```python
expected_t_r = 1.5
```

**Verification:**
```python
assert t_r == expected_t_r
```

### Step 5: Assign expected_t_r = 2.0

```python
expected_t_r = 2.0
```

### Step 6: Call add_metadata_to_bids_dataset()

```python
add_metadata_to_bids_dataset(bids_path=tmp_path / bids_path, metadata={'RepetitionTime': expected_t_r})
```

### Step 7: Assign t_r = infer_repetition_time_from_dataset(...)

```python
t_r = infer_repetition_time_from_dataset(bids_path=tmp_path / bids_path / 'derivatives', filters=[('task', 'main'), ('run', '01')])
```

**Verification:**
```python
assert t_r == expected_t_r
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test inferring repetition time from the BIDS dataset.\n\n    When using create_fake_bids_dataset the value is 1.5 secs by default\n    in the raw dataset.\n    When using add_metadata_to_bids_dataset the value is 2.0 secs.\n    '
bids_path = create_fake_bids_dataset(base_dir=tmp_path, n_sub=1, n_ses=1, tasks=['main'], n_runs=[1])
t_r = infer_repetition_time_from_dataset(bids_path=tmp_path / bids_path, filters=[('task', 'main')])
expected_t_r = 1.5
assert t_r == expected_t_r
expected_t_r = 2.0
add_metadata_to_bids_dataset(bids_path=tmp_path / bids_path, metadata={'RepetitionTime': expected_t_r})
t_r = infer_repetition_time_from_dataset(bids_path=tmp_path / bids_path / 'derivatives', filters=[('task', 'main'), ('run', '01')])
assert t_r == expected_t_r
```

## Next Steps


---

*Source: test_query.py:67 | Complexity: Intermediate | Last updated: 2026-05-18*