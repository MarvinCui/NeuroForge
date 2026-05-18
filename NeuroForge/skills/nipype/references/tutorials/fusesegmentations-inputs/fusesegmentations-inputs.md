# How To: Fusesegmentations Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test FuseSegmentations inputs

## Prerequisites

**Required Modules:**
- `longitudinal`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_norms=dict(argstr='-n %s', mandatory=True), in_segmentations=dict(argstr='-a %s', mandatory=True), in_segmentations_noCC=dict(argstr='-c %s', mandatory=True), out_file=dict(extensions=None, mandatory=True, position=-1), subject_id=dict(argstr='%s', position=-3), subjects_dir=dict(), timepoints=dict(argstr='%s', mandatory=True, position=-2))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_norms=dict(argstr='-n %s', mandatory=True), in_segmentations=dict(argstr='-a %s', mandatory=True), in_segmentations_noCC=dict(argstr='-c %s', mandatory=True), out_file=dict(extensions=None, mandatory=True, position=-1), subject_id=dict(argstr='%s', position=-3), subjects_dir=dict(), timepoints=dict(argstr='%s', mandatory=True, position=-2))
```

## Next Steps


---

*Source: test_auto_FuseSegmentations.py:6 | Complexity: Beginner | Last updated: 2026-05-18*