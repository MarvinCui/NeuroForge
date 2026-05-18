# How To: Dwipreproc Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test DWIPreproc inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(align_seepi=dict(argstr='-align_seepi'), args=dict(argstr='%s'), bval_scale=dict(argstr='-bvalue_scaling %s'), eddy_mask=dict(argstr='-eddy_mask %s', extensions=None), eddy_options=dict(argstr='-eddy_options "%s"'), eddy_slspec=dict(argstr='-eddy_slspec %s', extensions=None), eddyqc_all=dict(argstr='-eddyqc_all %s'), eddyqc_text=dict(argstr='-eddyqc_text %s'), environ=dict(nohash=True, usedefault=True), grad_file=dict(argstr='-grad %s', extensions=None, xor=['grad_fsl']), grad_fsl=dict(argstr='-fslgrad %s %s', xor=['grad_file']), in_bval=dict(extensions=None), in_bvec=dict(argstr='-fslgrad %s %s', extensions=None), in_epi=dict(argstr='-se_epi %s', extensions=None), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=0), json_import=dict(argstr='-json_import %s', extensions=None), nthreads=dict(argstr='-nthreads %d', nohash=True), out_bval=dict(extensions=None), out_bvec=dict(argstr='-export_grad_fsl %s %s', extensions=None), out_file=dict(argstr='%s', extensions=None, mandatory=True, position=1, usedefault=True), out_grad_fsl=dict(argstr='-export_grad_fsl %s, %s'), out_grad_mrtrix=dict(argstr='-export_grad_mrtrix %s', extensions=None), pe_dir=dict(argstr='-pe_dir %s'), ro_time=dict(argstr='-readout_time %f'), rpe_options=dict(argstr='-rpe_%s', mandatory=True, position=2), topup_options=dict(argstr='-topup_options "%s"'))
```


## Complete Example

```python
# Workflow
input_map = dict(align_seepi=dict(argstr='-align_seepi'), args=dict(argstr='%s'), bval_scale=dict(argstr='-bvalue_scaling %s'), eddy_mask=dict(argstr='-eddy_mask %s', extensions=None), eddy_options=dict(argstr='-eddy_options "%s"'), eddy_slspec=dict(argstr='-eddy_slspec %s', extensions=None), eddyqc_all=dict(argstr='-eddyqc_all %s'), eddyqc_text=dict(argstr='-eddyqc_text %s'), environ=dict(nohash=True, usedefault=True), grad_file=dict(argstr='-grad %s', extensions=None, xor=['grad_fsl']), grad_fsl=dict(argstr='-fslgrad %s %s', xor=['grad_file']), in_bval=dict(extensions=None), in_bvec=dict(argstr='-fslgrad %s %s', extensions=None), in_epi=dict(argstr='-se_epi %s', extensions=None), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=0), json_import=dict(argstr='-json_import %s', extensions=None), nthreads=dict(argstr='-nthreads %d', nohash=True), out_bval=dict(extensions=None), out_bvec=dict(argstr='-export_grad_fsl %s %s', extensions=None), out_file=dict(argstr='%s', extensions=None, mandatory=True, position=1, usedefault=True), out_grad_fsl=dict(argstr='-export_grad_fsl %s, %s'), out_grad_mrtrix=dict(argstr='-export_grad_mrtrix %s', extensions=None), pe_dir=dict(argstr='-pe_dir %s'), ro_time=dict(argstr='-readout_time %f'), rpe_options=dict(argstr='-rpe_%s', mandatory=True, position=2), topup_options=dict(argstr='-topup_options "%s"'))
```

## Next Steps


---

*Source: test_auto_DWIPreproc.py:6 | Complexity: Beginner | Last updated: 2026-05-18*