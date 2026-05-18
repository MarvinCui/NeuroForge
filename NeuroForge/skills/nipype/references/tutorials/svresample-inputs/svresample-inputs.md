# How To: Svresample Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test SVResample inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(align=dict(argstr='-align %s'), args=dict(argstr='%s'), array_size=dict(argstr='-size %d %d %d', xor=['target_file']), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-in %s', extensions=None, mandatory=True), origin=dict(argstr='-origin %g %g %g', xor=['target_file']), out_file=dict(argstr='-out %s', extensions=None, keep_extension=True, name_source='in_file', name_template='%s_resampled'), target_file=dict(argstr='-target %s', extensions=None, xor=['array_size', 'voxel_size', 'origin']), voxel_size=dict(argstr='-vsize %g %g %g', xor=['target_file']))
```


## Complete Example

```python
# Workflow
input_map = dict(align=dict(argstr='-align %s'), args=dict(argstr='%s'), array_size=dict(argstr='-size %d %d %d', xor=['target_file']), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-in %s', extensions=None, mandatory=True), origin=dict(argstr='-origin %g %g %g', xor=['target_file']), out_file=dict(argstr='-out %s', extensions=None, keep_extension=True, name_source='in_file', name_template='%s_resampled'), target_file=dict(argstr='-target %s', extensions=None, xor=['array_size', 'voxel_size', 'origin']), voxel_size=dict(argstr='-vsize %g %g %g', xor=['target_file']))
```

## Next Steps


---

*Source: test_auto_SVResample.py:6 | Complexity: Beginner | Last updated: 2026-05-18*