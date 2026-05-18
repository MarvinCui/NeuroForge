# How To: Applydeformations Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test ApplyDeformations inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(deformation_field=dict(extensions=None, field='comp{1}.def', mandatory=True), in_files=dict(field='fnames', mandatory=True), interp=dict(field='interp'), matlab_cmd=dict(), mfile=dict(usedefault=True), paths=dict(), reference_volume=dict(extensions=['.hdr', '.img', '.img.gz', '.nii'], field='comp{2}.id.space', mandatory=True), use_mcr=dict(), use_v8struct=dict(min_ver='8', usedefault=True))
```


## Complete Example

```python
# Workflow
input_map = dict(deformation_field=dict(extensions=None, field='comp{1}.def', mandatory=True), in_files=dict(field='fnames', mandatory=True), interp=dict(field='interp'), matlab_cmd=dict(), mfile=dict(usedefault=True), paths=dict(), reference_volume=dict(extensions=['.hdr', '.img', '.img.gz', '.nii'], field='comp{2}.id.space', mandatory=True), use_mcr=dict(), use_v8struct=dict(min_ver='8', usedefault=True))
```

## Next Steps


---

*Source: test_auto_ApplyDeformations.py:6 | Complexity: Beginner | Last updated: 2026-05-18*