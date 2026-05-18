# How To: Newsegment Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test NewSegment inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(affine_regularization=dict(field='warp.affreg'), channel_files=dict(copyfile=False, field='channel', mandatory=True), channel_info=dict(field='channel'), matlab_cmd=dict(), mfile=dict(usedefault=True), paths=dict(), sampling_distance=dict(field='warp.samp'), tissues=dict(field='tissue'), use_mcr=dict(), use_v8struct=dict(min_ver='8', usedefault=True), warping_regularization=dict(field='warp.reg'), write_deformation_fields=dict(field='warp.write'))
```


## Complete Example

```python
# Workflow
input_map = dict(affine_regularization=dict(field='warp.affreg'), channel_files=dict(copyfile=False, field='channel', mandatory=True), channel_info=dict(field='channel'), matlab_cmd=dict(), mfile=dict(usedefault=True), paths=dict(), sampling_distance=dict(field='warp.samp'), tissues=dict(field='tissue'), use_mcr=dict(), use_v8struct=dict(min_ver='8', usedefault=True), warping_regularization=dict(field='warp.reg'), write_deformation_fields=dict(field='warp.write'))
```

## Next Steps


---

*Source: test_auto_NewSegment.py:6 | Complexity: Beginner | Last updated: 2026-05-18*