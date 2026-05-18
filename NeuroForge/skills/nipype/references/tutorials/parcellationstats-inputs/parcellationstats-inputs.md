# How To: Parcellationstats Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test ParcellationStats inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), aseg=dict(extensions=None, mandatory=True), brainmask=dict(extensions=None, mandatory=True), copy_inputs=dict(), cortex_label=dict(extensions=None), environ=dict(nohash=True, usedefault=True), hemisphere=dict(argstr='%s', mandatory=True, position=-2), in_annotation=dict(argstr='-a %s', extensions=None, xor=['in_label']), in_cortex=dict(argstr='-cortex %s', extensions=None), in_label=dict(argstr='-l %s', extensions=None, xor=['in_annotatoin', 'out_color']), lh_pial=dict(extensions=None, mandatory=True), lh_white=dict(extensions=None, mandatory=True), mgz=dict(argstr='-mgz'), out_color=dict(argstr='-c %s', extensions=None, genfile=True, xor=['in_label']), out_table=dict(argstr='-f %s', extensions=None, genfile=True, requires=['tabular_output']), rh_pial=dict(extensions=None, mandatory=True), rh_white=dict(extensions=None, mandatory=True), ribbon=dict(extensions=None, mandatory=True), subject_id=dict(argstr='%s', mandatory=True, position=-3, usedefault=True), subjects_dir=dict(), surface=dict(argstr='%s', position=-1), tabular_output=dict(argstr='-b'), th3=dict(argstr='-th3', requires=['cortex_label']), thickness=dict(extensions=None, mandatory=True), transform=dict(extensions=None, mandatory=True), wm=dict(extensions=None, mandatory=True))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), aseg=dict(extensions=None, mandatory=True), brainmask=dict(extensions=None, mandatory=True), copy_inputs=dict(), cortex_label=dict(extensions=None), environ=dict(nohash=True, usedefault=True), hemisphere=dict(argstr='%s', mandatory=True, position=-2), in_annotation=dict(argstr='-a %s', extensions=None, xor=['in_label']), in_cortex=dict(argstr='-cortex %s', extensions=None), in_label=dict(argstr='-l %s', extensions=None, xor=['in_annotatoin', 'out_color']), lh_pial=dict(extensions=None, mandatory=True), lh_white=dict(extensions=None, mandatory=True), mgz=dict(argstr='-mgz'), out_color=dict(argstr='-c %s', extensions=None, genfile=True, xor=['in_label']), out_table=dict(argstr='-f %s', extensions=None, genfile=True, requires=['tabular_output']), rh_pial=dict(extensions=None, mandatory=True), rh_white=dict(extensions=None, mandatory=True), ribbon=dict(extensions=None, mandatory=True), subject_id=dict(argstr='%s', mandatory=True, position=-3, usedefault=True), subjects_dir=dict(), surface=dict(argstr='%s', position=-1), tabular_output=dict(argstr='-b'), th3=dict(argstr='-th3', requires=['cortex_label']), thickness=dict(extensions=None, mandatory=True), transform=dict(extensions=None, mandatory=True), wm=dict(extensions=None, mandatory=True))
```

## Next Steps


---

*Source: test_auto_ParcellationStats.py:6 | Complexity: Beginner | Last updated: 2026-05-18*