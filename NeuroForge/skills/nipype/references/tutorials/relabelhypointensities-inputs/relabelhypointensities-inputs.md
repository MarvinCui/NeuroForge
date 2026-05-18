# How To: Relabelhypointensities Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test RelabelHypointensities inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), aseg=dict(argstr='%s', extensions=None, mandatory=True, position=-3), environ=dict(nohash=True, usedefault=True), lh_white=dict(copyfile=True, extensions=None, mandatory=True), out_file=dict(argstr='%s', extensions=None, hash_files=False, keep_extension=False, name_source=['aseg'], name_template='%s.hypos.mgz', position=-1), rh_white=dict(copyfile=True, extensions=None, mandatory=True), subjects_dir=dict(), surf_directory=dict(argstr='%s', position=-2, usedefault=True))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), aseg=dict(argstr='%s', extensions=None, mandatory=True, position=-3), environ=dict(nohash=True, usedefault=True), lh_white=dict(copyfile=True, extensions=None, mandatory=True), out_file=dict(argstr='%s', extensions=None, hash_files=False, keep_extension=False, name_source=['aseg'], name_template='%s.hypos.mgz', position=-1), rh_white=dict(copyfile=True, extensions=None, mandatory=True), subjects_dir=dict(), surf_directory=dict(argstr='%s', position=-2, usedefault=True))
```

## Next Steps


---

*Source: test_auto_RelabelHypointensities.py:6 | Complexity: Beginner | Last updated: 2026-05-18*