# How To: Realignunwarp Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test RealignUnwarp inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(est_basis_func=dict(field='uweoptions.basfcn'), est_first_order_effects=dict(field='uweoptions.fot'), est_jacobian_deformations=dict(field='uweoptions.jm'), est_num_of_iterations=dict(field='uweoptions.noi', usedefault=True), est_re_est_mov_par=dict(field='uweoptions.rem'), est_reg_factor=dict(field='uweoptions.lambda', usedefault=True), est_reg_order=dict(field='uweoptions.regorder'), est_second_order_effects=dict(field='uweoptions.sot'), est_taylor_expansion_point=dict(field='uweoptions.expround', usedefault=True), est_unwarp_fwhm=dict(field='uweoptions.uwfwhm'), fwhm=dict(field='eoptions.fwhm'), in_files=dict(copyfile=True, field='data.scans', mandatory=True), interp=dict(field='eoptions.einterp'), matlab_cmd=dict(), mfile=dict(usedefault=True), out_prefix=dict(field='uwroptions.prefix', usedefault=True), paths=dict(), phase_map=dict(copyfile=False, extensions=None, field='data.pmscan'), quality=dict(field='eoptions.quality'), register_to_mean=dict(field='eoptions.rtm'), reslice_interp=dict(field='uwroptions.rinterp'), reslice_mask=dict(field='uwroptions.mask'), reslice_which=dict(field='uwroptions.uwwhich', usedefault=True), reslice_wrap=dict(field='uwroptions.wrap'), separation=dict(field='eoptions.sep'), use_mcr=dict(), use_v8struct=dict(min_ver='8', usedefault=True), weight_img=dict(extensions=None, field='eoptions.weight'), wrap=dict(field='eoptions.ewrap'))
```


## Complete Example

```python
# Workflow
input_map = dict(est_basis_func=dict(field='uweoptions.basfcn'), est_first_order_effects=dict(field='uweoptions.fot'), est_jacobian_deformations=dict(field='uweoptions.jm'), est_num_of_iterations=dict(field='uweoptions.noi', usedefault=True), est_re_est_mov_par=dict(field='uweoptions.rem'), est_reg_factor=dict(field='uweoptions.lambda', usedefault=True), est_reg_order=dict(field='uweoptions.regorder'), est_second_order_effects=dict(field='uweoptions.sot'), est_taylor_expansion_point=dict(field='uweoptions.expround', usedefault=True), est_unwarp_fwhm=dict(field='uweoptions.uwfwhm'), fwhm=dict(field='eoptions.fwhm'), in_files=dict(copyfile=True, field='data.scans', mandatory=True), interp=dict(field='eoptions.einterp'), matlab_cmd=dict(), mfile=dict(usedefault=True), out_prefix=dict(field='uwroptions.prefix', usedefault=True), paths=dict(), phase_map=dict(copyfile=False, extensions=None, field='data.pmscan'), quality=dict(field='eoptions.quality'), register_to_mean=dict(field='eoptions.rtm'), reslice_interp=dict(field='uwroptions.rinterp'), reslice_mask=dict(field='uwroptions.mask'), reslice_which=dict(field='uwroptions.uwwhich', usedefault=True), reslice_wrap=dict(field='uwroptions.wrap'), separation=dict(field='eoptions.sep'), use_mcr=dict(), use_v8struct=dict(min_ver='8', usedefault=True), weight_img=dict(extensions=None, field='eoptions.weight'), wrap=dict(field='eoptions.ewrap'))
```

## Next Steps


---

*Source: test_auto_RealignUnwarp.py:6 | Complexity: Beginner | Last updated: 2026-05-18*