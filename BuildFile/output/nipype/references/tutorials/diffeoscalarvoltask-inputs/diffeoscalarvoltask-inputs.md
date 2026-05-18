# How To: Diffeoscalarvoltask Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test diffeoScalarVolTask inputs

## Prerequisites

**Required Modules:**
- `registration`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), flip=dict(argstr='-flip %d %d %d'), in_file=dict(argstr='-in %s', extensions=None, mandatory=True), interpolation=dict(argstr='-interp %s', usedefault=True), out_file=dict(argstr='-out %s', extensions=None, keep_extension=True, name_source='in_file', name_template='%s_diffeoxfmd'), resampling_type=dict(argstr='-type %s'), target=dict(argstr='-target %s', extensions=None, xor=['voxel_size']), transform=dict(argstr='-trans %s', extensions=None, mandatory=True), voxel_size=dict(argstr='-vsize %g %g %g', xor=['target']))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), flip=dict(argstr='-flip %d %d %d'), in_file=dict(argstr='-in %s', extensions=None, mandatory=True), interpolation=dict(argstr='-interp %s', usedefault=True), out_file=dict(argstr='-out %s', extensions=None, keep_extension=True, name_source='in_file', name_template='%s_diffeoxfmd'), resampling_type=dict(argstr='-type %s'), target=dict(argstr='-target %s', extensions=None, xor=['voxel_size']), transform=dict(argstr='-trans %s', extensions=None, mandatory=True), voxel_size=dict(argstr='-vsize %g %g %g', xor=['target']))
```

## Next Steps


---

*Source: test_auto_diffeoScalarVolTask.py:6 | Complexity: Beginner | Last updated: 2026-05-18*