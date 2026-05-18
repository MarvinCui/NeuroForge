# How To: Segmentcc Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test SegmentCC inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), copy_inputs=dict(), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-aseg %s', extensions=None, mandatory=True), in_norm=dict(extensions=None, mandatory=True), out_file=dict(argstr='-o %s', extensions=None, hash_files=False, keep_extension=False, name_source=['in_file'], name_template='%s.auto.mgz'), out_rotation=dict(argstr='-lta %s', extensions=None, mandatory=True), subject_id=dict(argstr='%s', mandatory=True, position=-1, usedefault=True), subjects_dir=dict())
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), copy_inputs=dict(), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-aseg %s', extensions=None, mandatory=True), in_norm=dict(extensions=None, mandatory=True), out_file=dict(argstr='-o %s', extensions=None, hash_files=False, keep_extension=False, name_source=['in_file'], name_template='%s.auto.mgz'), out_rotation=dict(argstr='-lta %s', extensions=None, mandatory=True), subject_id=dict(argstr='%s', mandatory=True, position=-1, usedefault=True), subjects_dir=dict())
```

## Next Steps


---

*Source: test_auto_SegmentCC.py:6 | Complexity: Beginner | Last updated: 2026-05-18*