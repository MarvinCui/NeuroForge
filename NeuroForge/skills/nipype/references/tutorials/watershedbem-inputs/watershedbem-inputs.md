# How To: Watershedbem Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test WatershedBEM inputs

## Prerequisites

**Required Modules:**
- `base`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), atlas_mode=dict(argstr='--atlas'), environ=dict(nohash=True, usedefault=True), overwrite=dict(argstr='--overwrite', usedefault=True), subject_id=dict(argstr='--subject %s', mandatory=True), subjects_dir=dict(mandatory=True, usedefault=True), volume=dict(argstr='--volume %s', usedefault=True))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), atlas_mode=dict(argstr='--atlas'), environ=dict(nohash=True, usedefault=True), overwrite=dict(argstr='--overwrite', usedefault=True), subject_id=dict(argstr='--subject %s', mandatory=True), subjects_dir=dict(mandatory=True, usedefault=True), volume=dict(argstr='--volume %s', usedefault=True))
```

## Next Steps


---

*Source: test_auto_WatershedBEM.py:6 | Complexity: Beginner | Last updated: 2026-05-18*