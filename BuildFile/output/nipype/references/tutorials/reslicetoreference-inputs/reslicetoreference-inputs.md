# How To: Reslicetoreference Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test ResliceToReference inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(bounding_box=dict(field='comp{2}.idbbvox.bb'), in_files=dict(field='fnames', mandatory=True), interpolation=dict(field='interp'), matlab_cmd=dict(), mfile=dict(usedefault=True), paths=dict(), target=dict(extensions=None, field='comp{1}.id.space'), use_mcr=dict(), use_v8struct=dict(min_ver='8', usedefault=True), voxel_sizes=dict(field='comp{2}.idbbvox.vox'))
```


## Complete Example

```python
# Workflow
input_map = dict(bounding_box=dict(field='comp{2}.idbbvox.bb'), in_files=dict(field='fnames', mandatory=True), interpolation=dict(field='interp'), matlab_cmd=dict(), mfile=dict(usedefault=True), paths=dict(), target=dict(extensions=None, field='comp{1}.id.space'), use_mcr=dict(), use_v8struct=dict(min_ver='8', usedefault=True), voxel_sizes=dict(field='comp{2}.idbbvox.vox'))
```

## Next Steps


---

*Source: test_auto_ResliceToReference.py:6 | Complexity: Beginner | Last updated: 2026-05-18*