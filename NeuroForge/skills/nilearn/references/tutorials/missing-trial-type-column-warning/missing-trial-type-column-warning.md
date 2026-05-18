# How To: Missing Trial Type Column Warning

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Check that warning is thrown when an events file has no trial_type.

Ensure that the warning is thrown when running first_level_from_bids.

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
# Fixtures: tmp_path_factory
```

## Step-by-Step Guide

### Step 1: 'Check that warning is thrown when an events file has no trial_type.\n\n    Ensure that the warning is thrown when running first_level_from_bids.\n    '

```python
'Check that warning is thrown when an events file has no trial_type.\n\n    Ensure that the warning is thrown when running first_level_from_bids.\n    '
```

**Verification:**
```python
assert any(("No column named 'trial_type' found" in r.message.args[0] for r in record))
```

### Step 2: Assign bids_dataset = _new_bids_dataset(...)

```python
bids_dataset = _new_bids_dataset(tmp_path_factory.mktemp('one_event_missing'))
```

### Step 3: Assign events_files = get_bids_files(...)

```python
events_files = get_bids_files(main_path=bids_dataset, file_tag='events')
```

### Step 4: Assign events = pd.read_csv(...)

```python
events = pd.read_csv(events_files[0], sep='\t')
```

### Step 5: Assign events = events.drop(...)

```python
events = events.drop(columns='trial_type')
```

### Step 6: Call events.to_csv()

```python
events.to_csv(events_files[0], sep='\t', index=False)
```

### Step 7: Call first_level_from_bids()

```python
first_level_from_bids(dataset_path=bids_dataset, task_label='main', space_label='MNI', slice_time_ref=None)
```

**Verification:**
```python
assert any(("No column named 'trial_type' found" in r.message.args[0] for r in record))
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path_factory

# Workflow
'Check that warning is thrown when an events file has no trial_type.\n\n    Ensure that the warning is thrown when running first_level_from_bids.\n    '
bids_dataset = _new_bids_dataset(tmp_path_factory.mktemp('one_event_missing'))
events_files = get_bids_files(main_path=bids_dataset, file_tag='events')
events = pd.read_csv(events_files[0], sep='\t')
events = events.drop(columns='trial_type')
events.to_csv(events_files[0], sep='\t', index=False)
with pytest.warns() as record:
    first_level_from_bids(dataset_path=bids_dataset, task_label='main', space_label='MNI', slice_time_ref=None)
    assert any(("No column named 'trial_type' found" in r.message.args[0] for r in record))
```

## Next Steps


---

*Source: test_first_level_from_bids.py:819 | Complexity: Intermediate | Last updated: 2026-05-18*