# How To: Regtools Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test RegTools inputs

## Prerequisites

**Required Modules:**
- `regutils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(add_val=dict(argstr='-add %s'), args=dict(argstr='%s'), bin_flag=dict(argstr='-bin'), chg_res_val=dict(argstr='-chgres %f %f %f'), div_val=dict(argstr='-div %s'), down_flag=dict(argstr='-down'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-in %s', extensions=None, mandatory=True), inter_val=dict(argstr='-interp %d'), iso_flag=dict(argstr='-iso'), mask_file=dict(argstr='-nan %s', extensions=None), mul_val=dict(argstr='-mul %s'), noscl_flag=dict(argstr='-noscl'), omp_core_val=dict(argstr='-omp %i', usedefault=True), out_file=dict(argstr='-out %s', extensions=None, name_source=['in_file'], name_template='%s_tools.nii.gz'), rms_val=dict(argstr='-rms %s', extensions=None), smo_g_val=dict(argstr='-smoG %f %f %f'), smo_s_val=dict(argstr='-smoS %f %f %f'), sub_val=dict(argstr='-sub %s'), thr_val=dict(argstr='-thr %f'))
```


## Complete Example

```python
# Workflow
input_map = dict(add_val=dict(argstr='-add %s'), args=dict(argstr='%s'), bin_flag=dict(argstr='-bin'), chg_res_val=dict(argstr='-chgres %f %f %f'), div_val=dict(argstr='-div %s'), down_flag=dict(argstr='-down'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-in %s', extensions=None, mandatory=True), inter_val=dict(argstr='-interp %d'), iso_flag=dict(argstr='-iso'), mask_file=dict(argstr='-nan %s', extensions=None), mul_val=dict(argstr='-mul %s'), noscl_flag=dict(argstr='-noscl'), omp_core_val=dict(argstr='-omp %i', usedefault=True), out_file=dict(argstr='-out %s', extensions=None, name_source=['in_file'], name_template='%s_tools.nii.gz'), rms_val=dict(argstr='-rms %s', extensions=None), smo_g_val=dict(argstr='-smoG %f %f %f'), smo_s_val=dict(argstr='-smoS %f %f %f'), sub_val=dict(argstr='-sub %s'), thr_val=dict(argstr='-thr %f'))
```

## Next Steps


---

*Source: test_auto_RegTools.py:6 | Complexity: Beginner | Last updated: 2026-05-18*