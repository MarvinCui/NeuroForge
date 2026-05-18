# How To: Complex Relpaths Dataset

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Create a BIDS dataset with complex relative paths for testing.

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

### Step 1: 'Create a BIDS dataset with complex relative paths for testing.'

```python
'Create a BIDS dataset with complex relative paths for testing.'
```

### Step 2: Assign bids_dir = value

```python
bids_dir = tmpdir / 'test_group_dwi_scans_with_complex_relpaths'
```

### Step 3: Assign dset_yaml = os.path.join(...)

```python
dset_yaml = os.path.join(get_test_data_path(), 'skeleton_complex_relpaths.yml')
```

### Step 4: Call generate_bids_skeleton()

```python
generate_bids_skeleton(str(bids_dir), dset_yaml)
```

### Step 5: Assign layout = BIDSLayout(...)

```python
layout = BIDSLayout(str(bids_dir))
```

### Step 6: Assign subject_data = value

```python
subject_data = {'dwi': layout.get(suffix='dwi', extension='nii.gz', return_type='file')}
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir

# Workflow
'Create a BIDS dataset with complex relative paths for testing.'
bids_dir = tmpdir / 'test_group_dwi_scans_with_complex_relpaths'
dset_yaml = os.path.join(get_test_data_path(), 'skeleton_complex_relpaths.yml')
generate_bids_skeleton(str(bids_dir), dset_yaml)
layout = BIDSLayout(str(bids_dir))
subject_data = {'dwi': layout.get(suffix='dwi', extension='nii.gz', return_type='file')}
return (layout, subject_data)
```

## Next Steps


---

*Source: test_utils_grouping.py:399 | Complexity: Intermediate | Last updated: 2026-05-18*