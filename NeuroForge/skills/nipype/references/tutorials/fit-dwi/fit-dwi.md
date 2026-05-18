# How To: Fit Dwi

**Difficulty**: Beginner
**Estimated Time**: 5 minutes
**Tags**: pytest

## Overview

Instantiate format: Testing FitDwi interface.

## Prerequisites

**Required Modules:**
- `pytest`
- `testing`
- `niftyreg`
- `dwi`
- `niftyreg.tests.test_regutils`


## Step-by-Step Guide

### Step 1: Assign expected_cmd = cmd_tmp.format(...)

```python
expected_cmd = cmd_tmp.format(cmd=cmd, in_file=in_file, bval=bval_file, bvec=bvec_file, error='dwi_error.nii.gz', fa='dwi_famap.nii.gz', mc='dwi_mcmap.nii.gz', md='dwi_mdmap.nii.gz', nodiff='dwi_no_diff.nii.gz', res='dwi_resmap.nii.gz', rgb='dwi_rgbmap.nii.gz', syn='dwi_syn.nii.gz', ten2='dwi_tenmap2.nii.gz', v1='dwi_v1map.nii.gz', mcout='dwi_mcout.txt')
```


## Complete Example

```python
# Workflow
expected_cmd = cmd_tmp.format(cmd=cmd, in_file=in_file, bval=bval_file, bvec=bvec_file, error='dwi_error.nii.gz', fa='dwi_famap.nii.gz', mc='dwi_mcmap.nii.gz', md='dwi_mdmap.nii.gz', nodiff='dwi_no_diff.nii.gz', res='dwi_resmap.nii.gz', rgb='dwi_rgbmap.nii.gz', syn='dwi_syn.nii.gz', ten2='dwi_tenmap2.nii.gz', v1='dwi_v1map.nii.gz', mcout='dwi_mcout.txt')
```

## Next Steps


---

*Source: test_dwi.py:40 | Complexity: Beginner | Last updated: 2026-05-18*