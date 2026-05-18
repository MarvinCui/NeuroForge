# How To: Get Fieldmaps Bidsuri

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test get fieldmaps bidsuri

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

### Step 1: Assign base_dir = tmp_path_factory.mktemp(...)

```python
base_dir = tmp_path_factory.mktemp('test_get_fieldmaps_bidsuri')
```

**Verification:**
```python
assert len(fieldmaps) == 1
```

### Step 2: Assign bids_dir = value

```python
bids_dir = base_dir / 'dset_fmap_intendedfor_bidsuri'
```

**Verification:**
```python
assert fieldmaps[0]['suffix'] == 'epi'
```

### Step 3: Call generate_bids_skeleton()

```python
generate_bids_skeleton(str(bids_dir), dset_fmap_intendedfor_bidsuri)
```

**Verification:**
```python
assert layout.get_file(fieldmaps[0]['epi']).get_metadata()['IntendedFor'] == ['bids::sub-01/dwi/sub-01_dir-AP_dwi.nii.gz']
```

### Step 4: Assign layout = BIDSLayout(...)

```python
layout = BIDSLayout(str(bids_dir))
```

### Step 5: Assign dwi_file = value

```python
dwi_file = layout.get(suffix='dwi', extension='nii.gz', return_type='file')[0]
```

### Step 6: Assign fieldmaps = layout.get_fieldmap(...)

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
base_dir = tmp_path_factory.mktemp('test_get_fieldmaps_bidsuri')
bids_dir = base_dir / 'dset_fmap_intendedfor_bidsuri'
generate_bids_skeleton(str(bids_dir), dset_fmap_intendedfor_bidsuri)
layout = BIDSLayout(str(bids_dir))
dwi_file = layout.get(suffix='dwi', extension='nii.gz', return_type='file')[0]
fieldmaps = layout.get_fieldmap(dwi_file, return_list=True)
assert len(fieldmaps) == 1
assert fieldmaps[0]['suffix'] == 'epi'
assert layout.get_file(fieldmaps[0]['epi']).get_metadata()['IntendedFor'] == ['bids::sub-01/dwi/sub-01_dir-AP_dwi.nii.gz']
```

## Next Steps


---

*Source: test_utils_grouping.py:209 | Complexity: Intermediate | Last updated: 2026-05-18*