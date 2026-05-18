# How To: Warppoints Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test WarpPoints inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), coord_mm=dict(argstr='-mm', xor=['coord_vox']), coord_vox=dict(argstr='-vox', xor=['coord_mm']), dest_file=dict(argstr='-dest %s', extensions=None, mandatory=True), environ=dict(nohash=True, usedefault=True), in_coords=dict(argstr='%s', extensions=None, mandatory=True, position=-1), out_file=dict(extensions=None, name_source='in_coords', name_template='%s_warped', output_name='out_file'), src_file=dict(argstr='-src %s', extensions=None, mandatory=True), warp_file=dict(argstr='-warp %s', extensions=None, xor=['xfm_file']), xfm_file=dict(argstr='-xfm %s', extensions=None, xor=['warp_file']))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), coord_mm=dict(argstr='-mm', xor=['coord_vox']), coord_vox=dict(argstr='-vox', xor=['coord_mm']), dest_file=dict(argstr='-dest %s', extensions=None, mandatory=True), environ=dict(nohash=True, usedefault=True), in_coords=dict(argstr='%s', extensions=None, mandatory=True, position=-1), out_file=dict(extensions=None, name_source='in_coords', name_template='%s_warped', output_name='out_file'), src_file=dict(argstr='-src %s', extensions=None, mandatory=True), warp_file=dict(argstr='-warp %s', extensions=None, xor=['xfm_file']), xfm_file=dict(argstr='-xfm %s', extensions=None, xor=['warp_file']))
```

## Next Steps


---

*Source: test_auto_WarpPoints.py:6 | Complexity: Beginner | Last updated: 2026-05-18*