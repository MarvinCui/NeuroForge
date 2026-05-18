# How To: Roigen Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test ROIGen inputs

## Prerequisites

**Required Modules:**
- `cmtk`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(LUT_file=dict(extensions=None, xor=['use_freesurfer_LUT']), aparc_aseg_file=dict(extensions=None, mandatory=True), freesurfer_dir=dict(requires=['use_freesurfer_LUT']), out_dict_file=dict(extensions=None, genfile=True), out_roi_file=dict(extensions=None, genfile=True), use_freesurfer_LUT=dict(xor=['LUT_file']))
```


## Complete Example

```python
# Workflow
input_map = dict(LUT_file=dict(extensions=None, xor=['use_freesurfer_LUT']), aparc_aseg_file=dict(extensions=None, mandatory=True), freesurfer_dir=dict(requires=['use_freesurfer_LUT']), out_dict_file=dict(extensions=None, genfile=True), out_roi_file=dict(extensions=None, genfile=True), use_freesurfer_LUT=dict(xor=['LUT_file']))
```

## Next Steps


---

*Source: test_auto_ROIGen.py:6 | Complexity: Beginner | Last updated: 2026-05-18*