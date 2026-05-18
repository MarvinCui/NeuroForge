# How To: Gtmseg Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test GTMSeg inputs

## Prerequisites

**Required Modules:**
- `petsurfer`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), colortable=dict(argstr='--ctab %s', extensions=None), ctx_annot=dict(argstr='--ctx-annot %s %i %i'), dmax=dict(argstr='--dmax %f'), environ=dict(nohash=True, usedefault=True), head=dict(argstr='--head %s'), keep_cc=dict(argstr='--keep-cc'), keep_hypo=dict(argstr='--keep-hypo'), no_pons=dict(argstr='--no-pons'), no_seg_stats=dict(argstr='--no-seg-stats'), no_vermis=dict(argstr='--no-vermis'), out_file=dict(argstr='--o %s', extensions=None, usedefault=True), output_upsampling_factor=dict(argstr='--output-usf %i'), subject_id=dict(argstr='--s %s', mandatory=True), subjects_dir=dict(), subseg_cblum_wm=dict(argstr='--subseg-cblum-wm'), subsegwm=dict(argstr='--subsegwm'), upsampling_factor=dict(argstr='--usf %i'), wm_annot=dict(argstr='--wm-annot %s %i %i'), xcerseg=dict(argstr='--xcerseg'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), colortable=dict(argstr='--ctab %s', extensions=None), ctx_annot=dict(argstr='--ctx-annot %s %i %i'), dmax=dict(argstr='--dmax %f'), environ=dict(nohash=True, usedefault=True), head=dict(argstr='--head %s'), keep_cc=dict(argstr='--keep-cc'), keep_hypo=dict(argstr='--keep-hypo'), no_pons=dict(argstr='--no-pons'), no_seg_stats=dict(argstr='--no-seg-stats'), no_vermis=dict(argstr='--no-vermis'), out_file=dict(argstr='--o %s', extensions=None, usedefault=True), output_upsampling_factor=dict(argstr='--output-usf %i'), subject_id=dict(argstr='--s %s', mandatory=True), subjects_dir=dict(), subseg_cblum_wm=dict(argstr='--subseg-cblum-wm'), subsegwm=dict(argstr='--subsegwm'), upsampling_factor=dict(argstr='--usf %i'), wm_annot=dict(argstr='--wm-annot %s %i %i'), xcerseg=dict(argstr='--xcerseg'))
```

## Next Steps


---

*Source: test_auto_GTMSeg.py:6 | Complexity: Beginner | Last updated: 2026-05-18*