# How To: Get Entity Groups Without Multipartid

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test the get_entity_groups function.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `pprint`
- `pytest`
- `bids.layout`
- `niworkflows.utils.testing`
- `qsiprep.tests.utils`
- `qsiprep.utils`

**Setup Required:**
```python
# Fixtures: tmpdir
```

## Step-by-Step Guide

### Step 1: 'Test the get_entity_groups function.'

```python
'Test the get_entity_groups function.'
```

### Step 2: Assign bids_dir = value

```python
bids_dir = tmpdir / 'test_get_entity_groups'
```

### Step 3: Call generate_bids_skeleton()

```python
generate_bids_skeleton(str(bids_dir), dset_entities)
```

### Step 4: Assign layout = BIDSLayout(...)

```python
layout = BIDSLayout(str(bids_dir))
```

### Step 5: Assign subject_data = value

```python
subject_data = {'dwi': layout.get(suffix='dwi', extension='nii.gz', return_type='file')}
```

### Step 6: Assign entity_groups = grouping.get_entity_groups(...)

```python
entity_groups = grouping.get_entity_groups(layout, subject_data, combine_all_dwis=True)
```

### Step 7: Assign expected = value

```python
expected = [['sub-01_acq-98dir_dir-AP_run-2_dwi.nii.gz', 'sub-01_acq-99dir_dir-AP_run-1_dwi.nii.gz', 'sub-01_acq-99dir_dir-AP_run-3_dwi.nii.gz']]
```

### Step 8: Call check_expected()

```python
check_expected(entity_groups, expected)
```

### Step 9: Assign entity_groups = grouping.get_entity_groups(...)

```python
entity_groups = grouping.get_entity_groups(layout, subject_data, combine_all_dwis=False)
```

### Step 10: Assign expected = value

```python
expected = [['sub-01_acq-98dir_dir-AP_run-2_dwi.nii.gz'], ['sub-01_acq-99dir_dir-AP_run-1_dwi.nii.gz'], ['sub-01_acq-99dir_dir-AP_run-3_dwi.nii.gz']]
```

### Step 11: Call check_expected()

```python
check_expected(entity_groups, expected)
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir

# Workflow
'Test the get_entity_groups function.'
bids_dir = tmpdir / 'test_get_entity_groups'
generate_bids_skeleton(str(bids_dir), dset_entities)
layout = BIDSLayout(str(bids_dir))
subject_data = {'dwi': layout.get(suffix='dwi', extension='nii.gz', return_type='file')}
entity_groups = grouping.get_entity_groups(layout, subject_data, combine_all_dwis=True)
expected = [['sub-01_acq-98dir_dir-AP_run-2_dwi.nii.gz', 'sub-01_acq-99dir_dir-AP_run-1_dwi.nii.gz', 'sub-01_acq-99dir_dir-AP_run-3_dwi.nii.gz']]
check_expected(entity_groups, expected)
entity_groups = grouping.get_entity_groups(layout, subject_data, combine_all_dwis=False)
expected = [['sub-01_acq-98dir_dir-AP_run-2_dwi.nii.gz'], ['sub-01_acq-99dir_dir-AP_run-1_dwi.nii.gz'], ['sub-01_acq-99dir_dir-AP_run-3_dwi.nii.gz']]
check_expected(entity_groups, expected)
```

## Next Steps


---

*Source: test_utils_grouping.py:166 | Complexity: Advanced | Last updated: 2026-05-18*