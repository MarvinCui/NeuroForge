# How To: Flameo Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test FLAMEO inputs

## Prerequisites

**Required Modules:**
- `model`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), burnin=dict(argstr='--burnin=%d'), cope_file=dict(argstr='--copefile=%s', extensions=None, mandatory=True), cov_split_file=dict(argstr='--covsplitfile=%s', extensions=None, mandatory=True), design_file=dict(argstr='--designfile=%s', extensions=None, mandatory=True), dof_var_cope_file=dict(argstr='--dofvarcopefile=%s', extensions=None), environ=dict(nohash=True, usedefault=True), f_con_file=dict(argstr='--fcontrastsfile=%s', extensions=None), fix_mean=dict(argstr='--fixmean'), infer_outliers=dict(argstr='--inferoutliers'), log_dir=dict(argstr='--ld=%s', usedefault=True), mask_file=dict(argstr='--maskfile=%s', extensions=None, mandatory=True), n_jumps=dict(argstr='--njumps=%d'), no_pe_outputs=dict(argstr='--nopeoutput'), outlier_iter=dict(argstr='--ioni=%d'), output_type=dict(), run_mode=dict(argstr='--runmode=%s', mandatory=True), sample_every=dict(argstr='--sampleevery=%d'), sigma_dofs=dict(argstr='--sigma_dofs=%d'), t_con_file=dict(argstr='--tcontrastsfile=%s', extensions=None, mandatory=True), var_cope_file=dict(argstr='--varcopefile=%s', extensions=None))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), burnin=dict(argstr='--burnin=%d'), cope_file=dict(argstr='--copefile=%s', extensions=None, mandatory=True), cov_split_file=dict(argstr='--covsplitfile=%s', extensions=None, mandatory=True), design_file=dict(argstr='--designfile=%s', extensions=None, mandatory=True), dof_var_cope_file=dict(argstr='--dofvarcopefile=%s', extensions=None), environ=dict(nohash=True, usedefault=True), f_con_file=dict(argstr='--fcontrastsfile=%s', extensions=None), fix_mean=dict(argstr='--fixmean'), infer_outliers=dict(argstr='--inferoutliers'), log_dir=dict(argstr='--ld=%s', usedefault=True), mask_file=dict(argstr='--maskfile=%s', extensions=None, mandatory=True), n_jumps=dict(argstr='--njumps=%d'), no_pe_outputs=dict(argstr='--nopeoutput'), outlier_iter=dict(argstr='--ioni=%d'), output_type=dict(), run_mode=dict(argstr='--runmode=%s', mandatory=True), sample_every=dict(argstr='--sampleevery=%d'), sigma_dofs=dict(argstr='--sigma_dofs=%d'), t_con_file=dict(argstr='--tcontrastsfile=%s', extensions=None, mandatory=True), var_cope_file=dict(argstr='--varcopefile=%s', extensions=None))
```

## Next Steps


---

*Source: test_auto_FLAMEO.py:6 | Complexity: Beginner | Last updated: 2026-05-18*