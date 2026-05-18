# How To: Makesurfaces Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test MakeSurfaces inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), copy_inputs=dict(), environ=dict(nohash=True, usedefault=True), fix_mtl=dict(argstr='-fix_mtl'), hemisphere=dict(argstr='%s', mandatory=True, position=-1), in_T1=dict(argstr='-T1 %s', extensions=None), in_aseg=dict(argstr='-aseg %s', extensions=None), in_filled=dict(extensions=None, mandatory=True), in_label=dict(extensions=None, xor=['noaparc']), in_orig=dict(argstr='-orig %s', extensions=None, mandatory=True), in_white=dict(extensions=None), in_wm=dict(extensions=None, mandatory=True), longitudinal=dict(argstr='-long'), maximum=dict(argstr='-max %.1f'), mgz=dict(argstr='-mgz'), no_white=dict(argstr='-nowhite'), noaparc=dict(argstr='-noaparc', xor=['in_label']), orig_pial=dict(argstr='-orig_pial %s', extensions=None, requires=['in_label']), orig_white=dict(argstr='-orig_white %s', extensions=None), subject_id=dict(argstr='%s', mandatory=True, position=-2, usedefault=True), subjects_dir=dict(), white=dict(argstr='-white %s'), white_only=dict(argstr='-whiteonly'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), copy_inputs=dict(), environ=dict(nohash=True, usedefault=True), fix_mtl=dict(argstr='-fix_mtl'), hemisphere=dict(argstr='%s', mandatory=True, position=-1), in_T1=dict(argstr='-T1 %s', extensions=None), in_aseg=dict(argstr='-aseg %s', extensions=None), in_filled=dict(extensions=None, mandatory=True), in_label=dict(extensions=None, xor=['noaparc']), in_orig=dict(argstr='-orig %s', extensions=None, mandatory=True), in_white=dict(extensions=None), in_wm=dict(extensions=None, mandatory=True), longitudinal=dict(argstr='-long'), maximum=dict(argstr='-max %.1f'), mgz=dict(argstr='-mgz'), no_white=dict(argstr='-nowhite'), noaparc=dict(argstr='-noaparc', xor=['in_label']), orig_pial=dict(argstr='-orig_pial %s', extensions=None, requires=['in_label']), orig_white=dict(argstr='-orig_white %s', extensions=None), subject_id=dict(argstr='%s', mandatory=True, position=-2, usedefault=True), subjects_dir=dict(), white=dict(argstr='-white %s'), white_only=dict(argstr='-whiteonly'))
```

## Next Steps


---

*Source: test_auto_MakeSurfaces.py:6 | Complexity: Beginner | Last updated: 2026-05-18*