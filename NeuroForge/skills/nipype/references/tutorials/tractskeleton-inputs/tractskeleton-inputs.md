# How To: Tractskeleton Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test TractSkeleton inputs

## Prerequisites

**Required Modules:**
- `dti`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(alt_data_file=dict(argstr='-a %s', extensions=None), alt_skeleton=dict(argstr='-s %s', extensions=None), args=dict(argstr='%s'), data_file=dict(extensions=None), distance_map=dict(extensions=None), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-i %s', extensions=None, mandatory=True), output_type=dict(), project_data=dict(argstr='-p %.3f %s %s %s %s', requires=['threshold', 'distance_map', 'data_file']), projected_data=dict(extensions=None), search_mask_file=dict(extensions=None, xor=['use_cingulum_mask']), skeleton_file=dict(argstr='-o %s'), threshold=dict(), use_cingulum_mask=dict(usedefault=True, xor=['search_mask_file']))
```


## Complete Example

```python
# Workflow
input_map = dict(alt_data_file=dict(argstr='-a %s', extensions=None), alt_skeleton=dict(argstr='-s %s', extensions=None), args=dict(argstr='%s'), data_file=dict(extensions=None), distance_map=dict(extensions=None), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-i %s', extensions=None, mandatory=True), output_type=dict(), project_data=dict(argstr='-p %.3f %s %s %s %s', requires=['threshold', 'distance_map', 'data_file']), projected_data=dict(extensions=None), search_mask_file=dict(extensions=None, xor=['use_cingulum_mask']), skeleton_file=dict(argstr='-o %s'), threshold=dict(), use_cingulum_mask=dict(usedefault=True, xor=['search_mask_file']))
```

## Next Steps


---

*Source: test_auto_TractSkeleton.py:6 | Complexity: Beginner | Last updated: 2026-05-18*