# How To: Group Dwi Scans With Complex B0Fields

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test the group_dwi_scans function.

In the test dataset, we have the following::

fmap/
    sub-01_dir-AP_epi.nii.gz
    sub-01_dir-PA_epi.nii.gz
dwi/
    sub-01_dir-AP_run-1_dwi.nii.gz
    sub-01_dir-AP_run-2_dwi.nii.gz
    sub-01_dir-PA_dwi.nii.gz

The first two DWI runs have different B0 field identifiers, but link to the same fieldmap.
The third DWI run has a different B0 field identifier, and links to a different fieldmap.

We expect the first two DWI runs to be grouped together, and the third DWI run to be grouped
separately, based on having the same phase encoding direction.

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

### Step 1: 'Test the group_dwi_scans function.\n\n    In the test dataset, we have the following::\n\n    fmap/\n        sub-01_dir-AP_epi.nii.gz\n        sub-01_dir-PA_epi.nii.gz\n    dwi/\n        sub-01_dir-AP_run-1_dwi.nii.gz\n        sub-01_dir-AP_run-2_dwi.nii.gz\n        sub-01_dir-PA_dwi.nii.gz\n\n    The first two DWI runs have different B0 field identifiers, but link to the same fieldmap.\n    The third DWI run has a different B0 field identifier, and links to a different fieldmap.\n\n    We expect the first two DWI runs to be grouped together, and the third DWI run to be grouped\n    separately, based on having the same phase encoding direction.\n    '

```python
'Test the group_dwi_scans function.\n\n    In the test dataset, we have the following::\n\n    fmap/\n        sub-01_dir-AP_epi.nii.gz\n        sub-01_dir-PA_epi.nii.gz\n    dwi/\n        sub-01_dir-AP_run-1_dwi.nii.gz\n        sub-01_dir-AP_run-2_dwi.nii.gz\n        sub-01_dir-PA_dwi.nii.gz\n\n    The first two DWI runs have different B0 field identifiers, but link to the same fieldmap.\n    The third DWI run has a different B0 field identifier, and links to a different fieldmap.\n\n    We expect the first two DWI runs to be grouped together, and the third DWI run to be grouped\n    separately, based on having the same phase encoding direction.\n    '
```

### Step 2: Assign bids_dir = value

```python
bids_dir = tmpdir / 'test_group_dwi_scans_with_complex_b0fields'
```

### Step 3: Assign dset_yaml = os.path.join(...)

```python
dset_yaml = os.path.join(get_test_data_path(), 'skeleton_complex_b0fields.yml')
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

### Step 7: Assign unknown = grouping.group_dwi_scans(...)

```python
scan_groups, _ = grouping.group_dwi_scans(layout=layout, subject_data=subject_data, combine_scans=True, ignore_fieldmaps=False)
```

### Step 8: Assign expected = value

```python
expected = [{'concatenated_bids_name': 'sub-01_dir-AP', 'dwi_series': ['sub-01_dir-AP_run-1_dwi.nii.gz', 'sub-01_dir-AP_run-2_dwi.nii.gz'], 'dwi_series_pedir': 'j', 'fieldmap_info': {'suffix': None}}, {'concatenated_bids_name': 'sub-01_dir-PA', 'dwi_series': ['sub-01_dir-PA_dwi.nii.gz'], 'dwi_series_pedir': 'j-', 'fieldmap_info': {'suffix': None}}]
```

### Step 9: Call check_expected()

```python
check_expected(scan_groups, expected)
```

### Step 10: Assign unknown = grouping.group_dwi_scans(...)

```python
scan_groups, _ = grouping.group_dwi_scans(layout=layout, subject_data=subject_data, combine_scans=True, ignore_fieldmaps=False)
```

### Step 11: Assign expected = value

```python
expected = [['sub-01_dir-AP_run-1_dwi.nii.gz', 'sub-01_dir-AP_run-2_dwi.nii.gz'], ['sub-01_dir-PA_dwi.nii.gz']]
```

### Step 12: Call check_expected()

```python
check_expected(scan_groups, expected)
```

### Step 13: Assign unknown = grouping.group_dwi_scans(...)

```python
scan_groups, _ = grouping.group_dwi_scans(layout=layout, subject_data=subject_data, combine_scans=False, ignore_fieldmaps=False)
```

### Step 14: Assign expected = value

```python
expected = [['sub-01_dir-AP_run-1_dwi.nii.gz', 'sub-01_dir-AP_run-2_dwi.nii.gz'], ['sub-01_dir-PA_dwi.nii.gz']]
```

### Step 15: Call check_expected()

```python
check_expected(scan_groups, expected)
```

### Step 16: Assign unknown = grouping.group_dwi_scans(...)

```python
scan_groups, _ = grouping.group_dwi_scans(layout=layout, subject_data=subject_data, combine_scans=False, ignore_fieldmaps=False)
```

### Step 17: Assign expected = value

```python
expected = [['sub-01_dir-AP_run-1_dwi.nii.gz', 'sub-01_dir-AP_run-2_dwi.nii.gz'], ['sub-01_dir-PA_dwi.nii.gz']]
```

### Step 18: Call check_expected()

```python
check_expected(scan_groups, expected)
```

### Step 19: Assign unknown = grouping.group_dwi_scans(...)

```python
scan_groups, _ = grouping.group_dwi_scans(layout=layout, subject_data=subject_data, combine_scans=True, ignore_fieldmaps=True)
```

### Step 20: Assign expected = value

```python
expected = [['sub-01_dir-AP_run-1_dwi.nii.gz', 'sub-01_dir-AP_run-2_dwi.nii.gz'], ['sub-01_dir-PA_dwi.nii.gz']]
```

### Step 21: Call check_expected()

```python
check_expected(scan_groups, expected)
```

### Step 22: Assign unknown = grouping.group_dwi_scans(...)

```python
scan_groups, _ = grouping.group_dwi_scans(layout=layout, subject_data=subject_data, combine_scans=True, ignore_fieldmaps=False)
```

### Step 23: Assign expected = value

```python
expected = [['sub-01_dir-AP_run-1_dwi.nii.gz', 'sub-01_dir-AP_run-2_dwi.nii.gz', 'sub-01_dir-PA_dwi.nii.gz']]
```

### Step 24: Call check_expected()

```python
check_expected(scan_groups, expected)
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir

# Workflow
'Test the group_dwi_scans function.\n\n    In the test dataset, we have the following::\n\n    fmap/\n        sub-01_dir-AP_epi.nii.gz\n        sub-01_dir-PA_epi.nii.gz\n    dwi/\n        sub-01_dir-AP_run-1_dwi.nii.gz\n        sub-01_dir-AP_run-2_dwi.nii.gz\n        sub-01_dir-PA_dwi.nii.gz\n\n    The first two DWI runs have different B0 field identifiers, but link to the same fieldmap.\n    The third DWI run has a different B0 field identifier, and links to a different fieldmap.\n\n    We expect the first two DWI runs to be grouped together, and the third DWI run to be grouped\n    separately, based on having the same phase encoding direction.\n    '
bids_dir = tmpdir / 'test_group_dwi_scans_with_complex_b0fields'
dset_yaml = os.path.join(get_test_data_path(), 'skeleton_complex_b0fields.yml')
generate_bids_skeleton(str(bids_dir), dset_yaml)
layout = BIDSLayout(str(bids_dir))
subject_data = {'dwi': layout.get(suffix='dwi', extension='nii.gz', return_type='file')}
scan_groups, _ = grouping.group_dwi_scans(layout=layout, subject_data=subject_data, combine_scans=True, ignore_fieldmaps=False)
expected = [{'concatenated_bids_name': 'sub-01_dir-AP', 'dwi_series': ['sub-01_dir-AP_run-1_dwi.nii.gz', 'sub-01_dir-AP_run-2_dwi.nii.gz'], 'dwi_series_pedir': 'j', 'fieldmap_info': {'suffix': None}}, {'concatenated_bids_name': 'sub-01_dir-PA', 'dwi_series': ['sub-01_dir-PA_dwi.nii.gz'], 'dwi_series_pedir': 'j-', 'fieldmap_info': {'suffix': None}}]
check_expected(scan_groups, expected)
scan_groups, _ = grouping.group_dwi_scans(layout=layout, subject_data=subject_data, combine_scans=True, ignore_fieldmaps=False)
expected = [['sub-01_dir-AP_run-1_dwi.nii.gz', 'sub-01_dir-AP_run-2_dwi.nii.gz'], ['sub-01_dir-PA_dwi.nii.gz']]
check_expected(scan_groups, expected)
scan_groups, _ = grouping.group_dwi_scans(layout=layout, subject_data=subject_data, combine_scans=False, ignore_fieldmaps=False)
expected = [['sub-01_dir-AP_run-1_dwi.nii.gz', 'sub-01_dir-AP_run-2_dwi.nii.gz'], ['sub-01_dir-PA_dwi.nii.gz']]
check_expected(scan_groups, expected)
scan_groups, _ = grouping.group_dwi_scans(layout=layout, subject_data=subject_data, combine_scans=False, ignore_fieldmaps=False)
expected = [['sub-01_dir-AP_run-1_dwi.nii.gz', 'sub-01_dir-AP_run-2_dwi.nii.gz'], ['sub-01_dir-PA_dwi.nii.gz']]
check_expected(scan_groups, expected)
scan_groups, _ = grouping.group_dwi_scans(layout=layout, subject_data=subject_data, combine_scans=True, ignore_fieldmaps=True)
expected = [['sub-01_dir-AP_run-1_dwi.nii.gz', 'sub-01_dir-AP_run-2_dwi.nii.gz'], ['sub-01_dir-PA_dwi.nii.gz']]
check_expected(scan_groups, expected)
scan_groups, _ = grouping.group_dwi_scans(layout=layout, subject_data=subject_data, combine_scans=True, ignore_fieldmaps=False)
expected = [['sub-01_dir-AP_run-1_dwi.nii.gz', 'sub-01_dir-AP_run-2_dwi.nii.gz', 'sub-01_dir-PA_dwi.nii.gz']]
check_expected(scan_groups, expected)
```

## Next Steps


---

*Source: test_utils_grouping.py:262 | Complexity: Advanced | Last updated: 2026-05-18*