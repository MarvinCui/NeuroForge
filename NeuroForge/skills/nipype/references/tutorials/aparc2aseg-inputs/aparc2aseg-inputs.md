# How To: Aparc2Aseg Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Aparc2Aseg inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(a2009s=dict(argstr='--a2009s'), args=dict(argstr='%s'), aseg=dict(argstr='--aseg %s', extensions=None), copy_inputs=dict(), ctxseg=dict(argstr='--ctxseg %s', extensions=None), environ=dict(nohash=True, usedefault=True), filled=dict(extensions=None), hypo_wm=dict(argstr='--hypo-as-wm'), label_wm=dict(argstr='--labelwm'), lh_annotation=dict(extensions=None, mandatory=True), lh_pial=dict(extensions=None, mandatory=True), lh_ribbon=dict(extensions=None, mandatory=True), lh_white=dict(extensions=None, mandatory=True), out_file=dict(argstr='--o %s', extensions=None, mandatory=True), rh_annotation=dict(extensions=None, mandatory=True), rh_pial=dict(extensions=None, mandatory=True), rh_ribbon=dict(extensions=None, mandatory=True), rh_white=dict(extensions=None, mandatory=True), ribbon=dict(extensions=None, mandatory=True), rip_unknown=dict(argstr='--rip-unknown'), subject_id=dict(argstr='--s %s', mandatory=True, usedefault=True), subjects_dir=dict(), volmask=dict(argstr='--volmask'))
```


## Complete Example

```python
# Workflow
input_map = dict(a2009s=dict(argstr='--a2009s'), args=dict(argstr='%s'), aseg=dict(argstr='--aseg %s', extensions=None), copy_inputs=dict(), ctxseg=dict(argstr='--ctxseg %s', extensions=None), environ=dict(nohash=True, usedefault=True), filled=dict(extensions=None), hypo_wm=dict(argstr='--hypo-as-wm'), label_wm=dict(argstr='--labelwm'), lh_annotation=dict(extensions=None, mandatory=True), lh_pial=dict(extensions=None, mandatory=True), lh_ribbon=dict(extensions=None, mandatory=True), lh_white=dict(extensions=None, mandatory=True), out_file=dict(argstr='--o %s', extensions=None, mandatory=True), rh_annotation=dict(extensions=None, mandatory=True), rh_pial=dict(extensions=None, mandatory=True), rh_ribbon=dict(extensions=None, mandatory=True), rh_white=dict(extensions=None, mandatory=True), ribbon=dict(extensions=None, mandatory=True), rip_unknown=dict(argstr='--rip-unknown'), subject_id=dict(argstr='--s %s', mandatory=True, usedefault=True), subjects_dir=dict(), volmask=dict(argstr='--volmask'))
```

## Next Steps


---

*Source: test_auto_Aparc2Aseg.py:6 | Complexity: Beginner | Last updated: 2026-05-18*