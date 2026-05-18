# How To: Regaladin Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test RegAladin inputs

## Prerequisites

**Required Modules:**
- `reg`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(aff_direct_flag=dict(argstr='-affDirect'), aff_file=dict(argstr='-aff %s', extensions=None, name_source=['flo_file'], name_template='%s_aff.txt'), args=dict(argstr='%s'), cog_flag=dict(argstr='-cog'), environ=dict(nohash=True, usedefault=True), flo_file=dict(argstr='-flo %s', extensions=None, mandatory=True), flo_low_val=dict(argstr='-floLowThr %f'), flo_up_val=dict(argstr='-floUpThr %f'), fmask_file=dict(argstr='-fmask %s', extensions=None), gpuid_val=dict(argstr='-gpuid %i'), i_val=dict(argstr='-pi %d'), in_aff_file=dict(argstr='-inaff %s', extensions=None), ln_val=dict(argstr='-ln %d'), lp_val=dict(argstr='-lp %d'), maxit_val=dict(argstr='-maxit %d'), nac_flag=dict(argstr='-nac'), nosym_flag=dict(argstr='-noSym'), omp_core_val=dict(argstr='-omp %i', usedefault=True), platform_val=dict(argstr='-platf %i'), ref_file=dict(argstr='-ref %s', extensions=None, mandatory=True), ref_low_val=dict(argstr='-refLowThr %f'), ref_up_val=dict(argstr='-refUpThr %f'), res_file=dict(argstr='-res %s', extensions=None, name_source=['flo_file'], name_template='%s_res.nii.gz'), rig_only_flag=dict(argstr='-rigOnly'), rmask_file=dict(argstr='-rmask %s', extensions=None), smoo_f_val=dict(argstr='-smooF %f'), smoo_r_val=dict(argstr='-smooR %f'), v_val=dict(argstr='-pv %d'), verbosity_off_flag=dict(argstr='-voff'))
```


## Complete Example

```python
# Workflow
input_map = dict(aff_direct_flag=dict(argstr='-affDirect'), aff_file=dict(argstr='-aff %s', extensions=None, name_source=['flo_file'], name_template='%s_aff.txt'), args=dict(argstr='%s'), cog_flag=dict(argstr='-cog'), environ=dict(nohash=True, usedefault=True), flo_file=dict(argstr='-flo %s', extensions=None, mandatory=True), flo_low_val=dict(argstr='-floLowThr %f'), flo_up_val=dict(argstr='-floUpThr %f'), fmask_file=dict(argstr='-fmask %s', extensions=None), gpuid_val=dict(argstr='-gpuid %i'), i_val=dict(argstr='-pi %d'), in_aff_file=dict(argstr='-inaff %s', extensions=None), ln_val=dict(argstr='-ln %d'), lp_val=dict(argstr='-lp %d'), maxit_val=dict(argstr='-maxit %d'), nac_flag=dict(argstr='-nac'), nosym_flag=dict(argstr='-noSym'), omp_core_val=dict(argstr='-omp %i', usedefault=True), platform_val=dict(argstr='-platf %i'), ref_file=dict(argstr='-ref %s', extensions=None, mandatory=True), ref_low_val=dict(argstr='-refLowThr %f'), ref_up_val=dict(argstr='-refUpThr %f'), res_file=dict(argstr='-res %s', extensions=None, name_source=['flo_file'], name_template='%s_res.nii.gz'), rig_only_flag=dict(argstr='-rigOnly'), rmask_file=dict(argstr='-rmask %s', extensions=None), smoo_f_val=dict(argstr='-smooF %f'), smoo_r_val=dict(argstr='-smooR %f'), v_val=dict(argstr='-pv %d'), verbosity_off_flag=dict(argstr='-voff'))
```

## Next Steps


---

*Source: test_auto_RegAladin.py:6 | Complexity: Beginner | Last updated: 2026-05-18*