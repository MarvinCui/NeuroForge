# How To: Volumemask Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test VolumeMask inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), aseg=dict(extensions=None, xor=['in_aseg']), copy_inputs=dict(), environ=dict(nohash=True, usedefault=True), in_aseg=dict(argstr='--aseg_name %s', extensions=None, xor=['aseg']), left_ribbonlabel=dict(argstr='--label_left_ribbon %d', mandatory=True), left_whitelabel=dict(argstr='--label_left_white %d', mandatory=True), lh_pial=dict(extensions=None, mandatory=True), lh_white=dict(extensions=None, mandatory=True), rh_pial=dict(extensions=None, mandatory=True), rh_white=dict(extensions=None, mandatory=True), right_ribbonlabel=dict(argstr='--label_right_ribbon %d', mandatory=True), right_whitelabel=dict(argstr='--label_right_white %d', mandatory=True), save_ribbon=dict(argstr='--save_ribbon'), subject_id=dict(argstr='%s', mandatory=True, position=-1, usedefault=True), subjects_dir=dict())
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), aseg=dict(extensions=None, xor=['in_aseg']), copy_inputs=dict(), environ=dict(nohash=True, usedefault=True), in_aseg=dict(argstr='--aseg_name %s', extensions=None, xor=['aseg']), left_ribbonlabel=dict(argstr='--label_left_ribbon %d', mandatory=True), left_whitelabel=dict(argstr='--label_left_white %d', mandatory=True), lh_pial=dict(extensions=None, mandatory=True), lh_white=dict(extensions=None, mandatory=True), rh_pial=dict(extensions=None, mandatory=True), rh_white=dict(extensions=None, mandatory=True), right_ribbonlabel=dict(argstr='--label_right_ribbon %d', mandatory=True), right_whitelabel=dict(argstr='--label_right_white %d', mandatory=True), save_ribbon=dict(argstr='--save_ribbon'), subject_id=dict(argstr='%s', mandatory=True, position=-1, usedefault=True), subjects_dir=dict())
```

## Next Steps


---

*Source: test_auto_VolumeMask.py:6 | Complexity: Beginner | Last updated: 2026-05-18*