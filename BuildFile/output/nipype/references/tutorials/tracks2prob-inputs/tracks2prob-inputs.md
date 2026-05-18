# How To: Tracks2Prob Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Tracks2Prob inputs

## Prerequisites

**Required Modules:**
- `tracking`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), colour=dict(argstr='-colour', position=3), environ=dict(nohash=True, usedefault=True), fraction=dict(argstr='-fraction', position=3), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), out_filename=dict(argstr='%s', extensions=None, genfile=True, position=-1), output_datatype=dict(argstr='-datatype %s', position=2), resample=dict(argstr='-resample %d', position=3, units='mm'), template_file=dict(argstr='-template %s', extensions=None, position=1), voxel_dims=dict(argstr='-vox %s', position=2, sep=','))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), colour=dict(argstr='-colour', position=3), environ=dict(nohash=True, usedefault=True), fraction=dict(argstr='-fraction', position=3), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), out_filename=dict(argstr='%s', extensions=None, genfile=True, position=-1), output_datatype=dict(argstr='-datatype %s', position=2), resample=dict(argstr='-resample %d', position=3, units='mm'), template_file=dict(argstr='-template %s', extensions=None, position=1), voxel_dims=dict(argstr='-vox %s', position=2, sep=','))
```

## Next Steps


---

*Source: test_auto_Tracks2Prob.py:6 | Complexity: Beginner | Last updated: 2026-05-18*