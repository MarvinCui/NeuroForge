# How To: Centermass Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test CenterMass inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(all_rois=dict(argstr='-all_rois'), args=dict(argstr='%s'), automask=dict(argstr='-automask'), cm_file=dict(argstr='> %s', extensions=None, hash_files=False, keep_extension=False, name_source='in_file', name_template='%s_cm.out', position=-1), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', copyfile=True, extensions=None, mandatory=True, position=-2), local_ijk=dict(argstr='-local_ijk'), mask_file=dict(argstr='-mask %s', extensions=None), roi_vals=dict(argstr='-roi_vals %s'), set_cm=dict(argstr='-set %f %f %f'))
```


## Complete Example

```python
# Workflow
input_map = dict(all_rois=dict(argstr='-all_rois'), args=dict(argstr='%s'), automask=dict(argstr='-automask'), cm_file=dict(argstr='> %s', extensions=None, hash_files=False, keep_extension=False, name_source='in_file', name_template='%s_cm.out', position=-1), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', copyfile=True, extensions=None, mandatory=True, position=-2), local_ijk=dict(argstr='-local_ijk'), mask_file=dict(argstr='-mask %s', extensions=None), roi_vals=dict(argstr='-roi_vals %s'), set_cm=dict(argstr='-set %f %f %f'))
```

## Next Steps


---

*Source: test_auto_CenterMass.py:6 | Complexity: Beginner | Last updated: 2026-05-18*