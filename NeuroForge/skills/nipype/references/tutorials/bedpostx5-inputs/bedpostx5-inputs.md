# How To: Bedpostx5 Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test BEDPOSTX5 inputs

## Prerequisites

**Required Modules:**
- `dti`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(all_ard=dict(argstr='--allard', xor=('no_ard', 'all_ard')), args=dict(argstr='%s'), burn_in=dict(argstr='-b %d', usedefault=True), burn_in_no_ard=dict(argstr='--burnin_noard=%d', usedefault=True), bvals=dict(extensions=None, mandatory=True), bvecs=dict(extensions=None, mandatory=True), cnlinear=dict(argstr='--cnonlinear', xor=('no_spat', 'non_linear', 'cnlinear')), dwi=dict(extensions=None, mandatory=True), environ=dict(nohash=True, usedefault=True), f0_ard=dict(argstr='--f0 --ardf0', xor=['f0_noard', 'f0_ard', 'all_ard']), f0_noard=dict(argstr='--f0', xor=['f0_noard', 'f0_ard']), force_dir=dict(argstr='--forcedir', usedefault=True), fudge=dict(argstr='-w %d'), grad_dev=dict(extensions=None), gradnonlin=dict(argstr='-g'), logdir=dict(argstr='--logdir=%s'), mask=dict(extensions=None, mandatory=True), model=dict(argstr='-model %d'), n_fibres=dict(argstr='-n %d', mandatory=True, usedefault=True), n_jumps=dict(argstr='-j %d', usedefault=True), no_ard=dict(argstr='--noard', xor=('no_ard', 'all_ard')), no_spat=dict(argstr='--nospat', xor=('no_spat', 'non_linear', 'cnlinear')), non_linear=dict(argstr='--nonlinear', xor=('no_spat', 'non_linear', 'cnlinear')), out_dir=dict(argstr='%s', mandatory=True, position=1, usedefault=True), output_type=dict(), rician=dict(argstr='--rician'), sample_every=dict(argstr='-s %d', usedefault=True), seed=dict(argstr='--seed=%d'), update_proposal_every=dict(argstr='--updateproposalevery=%d', usedefault=True), use_gpu=dict())
```


## Complete Example

```python
# Workflow
input_map = dict(all_ard=dict(argstr='--allard', xor=('no_ard', 'all_ard')), args=dict(argstr='%s'), burn_in=dict(argstr='-b %d', usedefault=True), burn_in_no_ard=dict(argstr='--burnin_noard=%d', usedefault=True), bvals=dict(extensions=None, mandatory=True), bvecs=dict(extensions=None, mandatory=True), cnlinear=dict(argstr='--cnonlinear', xor=('no_spat', 'non_linear', 'cnlinear')), dwi=dict(extensions=None, mandatory=True), environ=dict(nohash=True, usedefault=True), f0_ard=dict(argstr='--f0 --ardf0', xor=['f0_noard', 'f0_ard', 'all_ard']), f0_noard=dict(argstr='--f0', xor=['f0_noard', 'f0_ard']), force_dir=dict(argstr='--forcedir', usedefault=True), fudge=dict(argstr='-w %d'), grad_dev=dict(extensions=None), gradnonlin=dict(argstr='-g'), logdir=dict(argstr='--logdir=%s'), mask=dict(extensions=None, mandatory=True), model=dict(argstr='-model %d'), n_fibres=dict(argstr='-n %d', mandatory=True, usedefault=True), n_jumps=dict(argstr='-j %d', usedefault=True), no_ard=dict(argstr='--noard', xor=('no_ard', 'all_ard')), no_spat=dict(argstr='--nospat', xor=('no_spat', 'non_linear', 'cnlinear')), non_linear=dict(argstr='--nonlinear', xor=('no_spat', 'non_linear', 'cnlinear')), out_dir=dict(argstr='%s', mandatory=True, position=1, usedefault=True), output_type=dict(), rician=dict(argstr='--rician'), sample_every=dict(argstr='-s %d', usedefault=True), seed=dict(argstr='--seed=%d'), update_proposal_every=dict(argstr='--updateproposalevery=%d', usedefault=True), use_gpu=dict())
```

## Next Steps


---

*Source: test_auto_BEDPOSTX5.py:6 | Complexity: Beginner | Last updated: 2026-05-18*