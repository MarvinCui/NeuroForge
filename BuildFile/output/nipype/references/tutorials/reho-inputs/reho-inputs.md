# How To: Reho Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test ReHo inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), chi_sq=dict(argstr='-chi_sq'), ellipsoid=dict(argstr='-neigh_X %s -neigh_Y %s -neigh_Z %s', xor=['sphere', 'neighborhood']), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-inset %s', extensions=None, mandatory=True, position=1), label_set=dict(argstr='-in_rois %s', extensions=None), mask_file=dict(argstr='-mask %s', extensions=None), neighborhood=dict(argstr='-nneigh %s', xor=['sphere', 'ellipsoid']), out_file=dict(argstr='-prefix %s', extensions=None, keep_extension=True, name_source='in_file', name_template='%s_reho', position=0), overwrite=dict(argstr='-overwrite'), sphere=dict(argstr='-neigh_RAD %s', xor=['neighborhood', 'ellipsoid']))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), chi_sq=dict(argstr='-chi_sq'), ellipsoid=dict(argstr='-neigh_X %s -neigh_Y %s -neigh_Z %s', xor=['sphere', 'neighborhood']), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-inset %s', extensions=None, mandatory=True, position=1), label_set=dict(argstr='-in_rois %s', extensions=None), mask_file=dict(argstr='-mask %s', extensions=None), neighborhood=dict(argstr='-nneigh %s', xor=['sphere', 'ellipsoid']), out_file=dict(argstr='-prefix %s', extensions=None, keep_extension=True, name_source='in_file', name_template='%s_reho', position=0), overwrite=dict(argstr='-overwrite'), sphere=dict(argstr='-neigh_RAD %s', xor=['neighborhood', 'ellipsoid']))
```

## Next Steps


---

*Source: test_auto_ReHo.py:6 | Complexity: Beginner | Last updated: 2026-05-18*