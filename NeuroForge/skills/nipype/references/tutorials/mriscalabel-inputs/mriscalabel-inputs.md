# How To: Mriscalabel Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test MRIsCALabel inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), aseg=dict(argstr='-aseg %s', extensions=None), canonsurf=dict(argstr='%s', extensions=None, mandatory=True, position=-3), classifier=dict(argstr='%s', extensions=None, mandatory=True, position=-2), copy_inputs=dict(), curv=dict(extensions=None, mandatory=True), environ=dict(nohash=True, usedefault=True), hemisphere=dict(argstr='%s', mandatory=True, position=-4), label=dict(argstr='-l %s', extensions=None), num_threads=dict(), out_file=dict(argstr='%s', extensions=None, hash_files=False, keep_extension=True, name_source=['hemisphere'], name_template='%s.aparc.annot', position=-1), seed=dict(argstr='-seed %d'), smoothwm=dict(extensions=None, mandatory=True), subject_id=dict(argstr='%s', mandatory=True, position=-5, usedefault=True), subjects_dir=dict(), sulc=dict(extensions=None, mandatory=True))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), aseg=dict(argstr='-aseg %s', extensions=None), canonsurf=dict(argstr='%s', extensions=None, mandatory=True, position=-3), classifier=dict(argstr='%s', extensions=None, mandatory=True, position=-2), copy_inputs=dict(), curv=dict(extensions=None, mandatory=True), environ=dict(nohash=True, usedefault=True), hemisphere=dict(argstr='%s', mandatory=True, position=-4), label=dict(argstr='-l %s', extensions=None), num_threads=dict(), out_file=dict(argstr='%s', extensions=None, hash_files=False, keep_extension=True, name_source=['hemisphere'], name_template='%s.aparc.annot', position=-1), seed=dict(argstr='-seed %d'), smoothwm=dict(extensions=None, mandatory=True), subject_id=dict(argstr='%s', mandatory=True, position=-5, usedefault=True), subjects_dir=dict(), sulc=dict(extensions=None, mandatory=True))
```

## Next Steps


---

*Source: test_auto_MRIsCALabel.py:6 | Complexity: Beginner | Last updated: 2026-05-18*