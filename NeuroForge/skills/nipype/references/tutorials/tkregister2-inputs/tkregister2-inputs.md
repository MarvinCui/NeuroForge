# How To: Tkregister2 Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Tkregister2 inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), fsl_in_matrix=dict(argstr='--fsl %s', extensions=None), fsl_out=dict(argstr='--fslregout %s'), fstal=dict(argstr='--fstal', xor=['target_image', 'moving_image', 'reg_file']), fstarg=dict(argstr='--fstarg', xor=['target_image']), invert_lta_in=dict(requires=['lta_in']), invert_lta_out=dict(argstr='--ltaout-inv', requires=['lta_in']), lta_in=dict(argstr='--lta %s', extensions=None), lta_out=dict(argstr='--ltaout %s'), moving_image=dict(argstr='--mov %s', extensions=None, mandatory=True), movscale=dict(argstr='--movscale %f'), noedit=dict(argstr='--noedit', usedefault=True), reg_file=dict(argstr='--reg %s', extensions=None, mandatory=True, usedefault=True), reg_header=dict(argstr='--regheader'), subject_id=dict(argstr='--s %s'), subjects_dir=dict(), target_image=dict(argstr='--targ %s', extensions=None, xor=['fstarg']), xfm=dict(argstr='--xfm %s', extensions=None))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), fsl_in_matrix=dict(argstr='--fsl %s', extensions=None), fsl_out=dict(argstr='--fslregout %s'), fstal=dict(argstr='--fstal', xor=['target_image', 'moving_image', 'reg_file']), fstarg=dict(argstr='--fstarg', xor=['target_image']), invert_lta_in=dict(requires=['lta_in']), invert_lta_out=dict(argstr='--ltaout-inv', requires=['lta_in']), lta_in=dict(argstr='--lta %s', extensions=None), lta_out=dict(argstr='--ltaout %s'), moving_image=dict(argstr='--mov %s', extensions=None, mandatory=True), movscale=dict(argstr='--movscale %f'), noedit=dict(argstr='--noedit', usedefault=True), reg_file=dict(argstr='--reg %s', extensions=None, mandatory=True, usedefault=True), reg_header=dict(argstr='--regheader'), subject_id=dict(argstr='--s %s'), subjects_dir=dict(), target_image=dict(argstr='--targ %s', extensions=None, xor=['fstarg']), xfm=dict(argstr='--xfm %s', extensions=None))
```

## Next Steps


---

*Source: test_auto_Tkregister2.py:6 | Complexity: Beginner | Last updated: 2026-05-18*