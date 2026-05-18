# How To: Get Fieldmaps Relpaths

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test the get_fieldmaps function.

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
# Fixtures: tmp_path_factory
```

## Step-by-Step Guide

### Step 1: 'Test the get_fieldmaps function.'

```python
'Test the get_fieldmaps function.'
```

**Verification:**
```python
assert len(fieldmaps) == 1
```

### Step 2: Assign base_dir = tmp_path_factory.mktemp(...)

```python
base_dir = tmp_path_factory.mktemp('test_get_fieldmaps_relpaths')
```

**Verification:**
```python
assert fieldmaps[0]['suffix'] == 'epi'
```

### Step 3: Assign bids_dir = value

```python
bids_dir = base_dir / 'dset_fmap_intendedfor_relpath'
```

**Verification:**
```python
assert layout.get_file(fieldmaps[0]['epi']).get_metadata()['IntendedFor'] == ['dwi/sub-01_dir-AP_dwi.nii.gz']
```

### Step 4: Call generate_bids_skeleton()

```python
generate_bids_skeleton(str(bids_dir), dset_fmap_intendedfor_relpath)
```

### Step 5: Assign layout = BIDSLayout(...)

```python
layout = BIDSLayout(str(bids_dir))
```

### Step 6: Assign dwi_file = value

```python
dwi_file = layout.get(suffix='dwi', extension='nii.gz', return_type='file')[0]
```

### Step 7: Assign fieldmaps = layout.get_fieldmap(...)

```python
fieldmaps = layout.get_fieldmap(dwi_file, return_list=True)
```

**Verification:**
```python
assert len(fieldmaps) == 1
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path_factory

# Workflow
'Test the get_fieldmaps function.'
base_dir = tmp_path_factory.mktemp('test_get_fieldmaps_relpaths')
bids_dir = base_dir / 'dset_fmap_intendedfor_relpath'
generate_bids_skeleton(str(bids_dir), dset_fmap_intendedfor_relpath)
layout = BIDSLayout(str(bids_dir))
dwi_file = layout.get(suffix='dwi', extension='nii.gz', return_type='file')[0]
fieldmaps = layout.get_fieldmap(dwi_file, return_list=True)
assert len(fieldmaps) == 1
assert fieldmaps[0]['suffix'] == 'epi'
assert layout.get_file(fieldmaps[0]['epi']).get_metadata()['IntendedFor'] == ['dwi/sub-01_dir-AP_dwi.nii.gz']
```

## Next Steps


---

*Source: test_utils_grouping.py:191 | Complexity: Intermediate | Last updated: 2026-05-18*