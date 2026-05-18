# How To: Topup Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test TOPUP inputs

## Prerequisites

**Required Modules:**
- `epi`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), config=dict(argstr='--config=%s', usedefault=True), encoding_direction=dict(argstr='--datain=%s', mandatory=True, requires=['readout_times'], xor=['encoding_file']), encoding_file=dict(argstr='--datain=%s', extensions=None, mandatory=True, xor=['encoding_direction']), environ=dict(nohash=True, usedefault=True), estmov=dict(argstr='--estmov=%d'), fwhm=dict(argstr='--fwhm=%f'), in_file=dict(argstr='--imain=%s', extensions=None, mandatory=True), interp=dict(argstr='--interp=%s'), max_iter=dict(argstr='--miter=%d'), minmet=dict(argstr='--minmet=%d'), numprec=dict(argstr='--numprec=%s'), out_base=dict(argstr='--out=%s', extensions=None, hash_files=False, name_source=['in_file'], name_template='%s_base'), out_corrected=dict(argstr='--iout=%s', extensions=None, hash_files=False, name_source=['in_file'], name_template='%s_corrected'), out_field=dict(argstr='--fout=%s', extensions=None, hash_files=False, name_source=['in_file'], name_template='%s_field'), out_jac_prefix=dict(argstr='--jacout=%s', hash_files=False, usedefault=True), out_logfile=dict(argstr='--logout=%s', extensions=None, hash_files=False, keep_extension=True, name_source=['in_file'], name_template='%s_topup.log'), out_mat_prefix=dict(argstr='--rbmout=%s', hash_files=False, usedefault=True), out_warp_prefix=dict(argstr='--dfout=%s', hash_files=False, usedefault=True), output_type=dict(), readout_times=dict(mandatory=True, requires=['encoding_direction'], xor=['encoding_file']), reg_lambda=dict(argstr='--lambda=%0.f'), regmod=dict(argstr='--regmod=%s'), regrid=dict(argstr='--regrid=%d'), scale=dict(argstr='--scale=%d'), splineorder=dict(argstr='--splineorder=%d'), ssqlambda=dict(argstr='--ssqlambda=%d'), subsamp=dict(argstr='--subsamp=%d'), warp_res=dict(argstr='--warpres=%f'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), config=dict(argstr='--config=%s', usedefault=True), encoding_direction=dict(argstr='--datain=%s', mandatory=True, requires=['readout_times'], xor=['encoding_file']), encoding_file=dict(argstr='--datain=%s', extensions=None, mandatory=True, xor=['encoding_direction']), environ=dict(nohash=True, usedefault=True), estmov=dict(argstr='--estmov=%d'), fwhm=dict(argstr='--fwhm=%f'), in_file=dict(argstr='--imain=%s', extensions=None, mandatory=True), interp=dict(argstr='--interp=%s'), max_iter=dict(argstr='--miter=%d'), minmet=dict(argstr='--minmet=%d'), numprec=dict(argstr='--numprec=%s'), out_base=dict(argstr='--out=%s', extensions=None, hash_files=False, name_source=['in_file'], name_template='%s_base'), out_corrected=dict(argstr='--iout=%s', extensions=None, hash_files=False, name_source=['in_file'], name_template='%s_corrected'), out_field=dict(argstr='--fout=%s', extensions=None, hash_files=False, name_source=['in_file'], name_template='%s_field'), out_jac_prefix=dict(argstr='--jacout=%s', hash_files=False, usedefault=True), out_logfile=dict(argstr='--logout=%s', extensions=None, hash_files=False, keep_extension=True, name_source=['in_file'], name_template='%s_topup.log'), out_mat_prefix=dict(argstr='--rbmout=%s', hash_files=False, usedefault=True), out_warp_prefix=dict(argstr='--dfout=%s', hash_files=False, usedefault=True), output_type=dict(), readout_times=dict(mandatory=True, requires=['encoding_direction'], xor=['encoding_file']), reg_lambda=dict(argstr='--lambda=%0.f'), regmod=dict(argstr='--regmod=%s'), regrid=dict(argstr='--regrid=%d'), scale=dict(argstr='--scale=%d'), splineorder=dict(argstr='--splineorder=%d'), ssqlambda=dict(argstr='--ssqlambda=%d'), subsamp=dict(argstr='--subsamp=%d'), warp_res=dict(argstr='--warpres=%f'))
```

## Next Steps


---

*Source: test_auto_TOPUP.py:6 | Complexity: Beginner | Last updated: 2026-05-18*