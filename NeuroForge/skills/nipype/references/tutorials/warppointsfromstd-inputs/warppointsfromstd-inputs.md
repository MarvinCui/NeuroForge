# How To: Warppointsfromstd Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test WarpPointsFromStd inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), coord_mm=dict(argstr='-mm', xor=['coord_vox']), coord_vox=dict(argstr='-vox', xor=['coord_mm']), environ=dict(nohash=True, usedefault=True), img_file=dict(argstr='-img %s', extensions=None, mandatory=True), in_coords=dict(argstr='%s', extensions=None, mandatory=True, position=-2), std_file=dict(argstr='-std %s', extensions=None, mandatory=True), warp_file=dict(argstr='-warp %s', extensions=None, xor=['xfm_file']), xfm_file=dict(argstr='-xfm %s', extensions=None, xor=['warp_file']))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), coord_mm=dict(argstr='-mm', xor=['coord_vox']), coord_vox=dict(argstr='-vox', xor=['coord_mm']), environ=dict(nohash=True, usedefault=True), img_file=dict(argstr='-img %s', extensions=None, mandatory=True), in_coords=dict(argstr='%s', extensions=None, mandatory=True, position=-2), std_file=dict(argstr='-std %s', extensions=None, mandatory=True), warp_file=dict(argstr='-warp %s', extensions=None, xor=['xfm_file']), xfm_file=dict(argstr='-xfm %s', extensions=None, xor=['warp_file']))
```

## Next Steps


---

*Source: test_auto_WarpPointsFromStd.py:6 | Complexity: Beginner | Last updated: 2026-05-18*