# How To: Applyvoltransform Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test ApplyVolTransform inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), fs_target=dict(argstr='--fstarg', mandatory=True, requires=['reg_file'], xor=('target_file', 'tal', 'fs_target')), fsl_reg_file=dict(argstr='--fsl %s', extensions=None, mandatory=True, xor=('reg_file', 'lta_file', 'lta_inv_file', 'fsl_reg_file', 'xfm_reg_file', 'reg_header', 'mni_152_reg', 'subject')), interp=dict(argstr='--interp %s'), inverse=dict(argstr='--inv'), invert_morph=dict(argstr='--inv-morph', requires=['m3z_file']), lta_file=dict(argstr='--lta %s', extensions=None, mandatory=True, xor=('reg_file', 'lta_file', 'lta_inv_file', 'fsl_reg_file', 'xfm_reg_file', 'reg_header', 'mni_152_reg', 'subject')), lta_inv_file=dict(argstr='--lta-inv %s', extensions=None, mandatory=True, xor=('reg_file', 'lta_file', 'lta_inv_file', 'fsl_reg_file', 'xfm_reg_file', 'reg_header', 'mni_152_reg', 'subject')), m3z_file=dict(argstr='--m3z %s', extensions=None), mni_152_reg=dict(argstr='--regheader', mandatory=True, xor=('reg_file', 'lta_file', 'lta_inv_file', 'fsl_reg_file', 'xfm_reg_file', 'reg_header', 'mni_152_reg', 'subject')), no_ded_m3z_path=dict(argstr='--noDefM3zPath', requires=['m3z_file']), no_resample=dict(argstr='--no-resample'), reg_file=dict(argstr='--reg %s', extensions=None, mandatory=True, xor=('reg_file', 'lta_file', 'lta_inv_file', 'fsl_reg_file', 'xfm_reg_file', 'reg_header', 'mni_152_reg', 'subject')), reg_header=dict(argstr='--regheader', mandatory=True, xor=('reg_file', 'lta_file', 'lta_inv_file', 'fsl_reg_file', 'xfm_reg_file', 'reg_header', 'mni_152_reg', 'subject')), source_file=dict(argstr='--mov %s', copyfile=False, extensions=None, mandatory=True), subject=dict(argstr='--s %s', mandatory=True, xor=('reg_file', 'lta_file', 'lta_inv_file', 'fsl_reg_file', 'xfm_reg_file', 'reg_header', 'mni_152_reg', 'subject')), subjects_dir=dict(), tal=dict(argstr='--tal', mandatory=True, xor=('target_file', 'tal', 'fs_target')), tal_resolution=dict(argstr='--talres %.10f'), target_file=dict(argstr='--targ %s', extensions=None, mandatory=True, xor=('target_file', 'tal', 'fs_target')), transformed_file=dict(argstr='--o %s', extensions=None, genfile=True), xfm_reg_file=dict(argstr='--xfm %s', extensions=None, mandatory=True, xor=('reg_file', 'lta_file', 'lta_inv_file', 'fsl_reg_file', 'xfm_reg_file', 'reg_header', 'mni_152_reg', 'subject')))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), fs_target=dict(argstr='--fstarg', mandatory=True, requires=['reg_file'], xor=('target_file', 'tal', 'fs_target')), fsl_reg_file=dict(argstr='--fsl %s', extensions=None, mandatory=True, xor=('reg_file', 'lta_file', 'lta_inv_file', 'fsl_reg_file', 'xfm_reg_file', 'reg_header', 'mni_152_reg', 'subject')), interp=dict(argstr='--interp %s'), inverse=dict(argstr='--inv'), invert_morph=dict(argstr='--inv-morph', requires=['m3z_file']), lta_file=dict(argstr='--lta %s', extensions=None, mandatory=True, xor=('reg_file', 'lta_file', 'lta_inv_file', 'fsl_reg_file', 'xfm_reg_file', 'reg_header', 'mni_152_reg', 'subject')), lta_inv_file=dict(argstr='--lta-inv %s', extensions=None, mandatory=True, xor=('reg_file', 'lta_file', 'lta_inv_file', 'fsl_reg_file', 'xfm_reg_file', 'reg_header', 'mni_152_reg', 'subject')), m3z_file=dict(argstr='--m3z %s', extensions=None), mni_152_reg=dict(argstr='--regheader', mandatory=True, xor=('reg_file', 'lta_file', 'lta_inv_file', 'fsl_reg_file', 'xfm_reg_file', 'reg_header', 'mni_152_reg', 'subject')), no_ded_m3z_path=dict(argstr='--noDefM3zPath', requires=['m3z_file']), no_resample=dict(argstr='--no-resample'), reg_file=dict(argstr='--reg %s', extensions=None, mandatory=True, xor=('reg_file', 'lta_file', 'lta_inv_file', 'fsl_reg_file', 'xfm_reg_file', 'reg_header', 'mni_152_reg', 'subject')), reg_header=dict(argstr='--regheader', mandatory=True, xor=('reg_file', 'lta_file', 'lta_inv_file', 'fsl_reg_file', 'xfm_reg_file', 'reg_header', 'mni_152_reg', 'subject')), source_file=dict(argstr='--mov %s', copyfile=False, extensions=None, mandatory=True), subject=dict(argstr='--s %s', mandatory=True, xor=('reg_file', 'lta_file', 'lta_inv_file', 'fsl_reg_file', 'xfm_reg_file', 'reg_header', 'mni_152_reg', 'subject')), subjects_dir=dict(), tal=dict(argstr='--tal', mandatory=True, xor=('target_file', 'tal', 'fs_target')), tal_resolution=dict(argstr='--talres %.10f'), target_file=dict(argstr='--targ %s', extensions=None, mandatory=True, xor=('target_file', 'tal', 'fs_target')), transformed_file=dict(argstr='--o %s', extensions=None, genfile=True), xfm_reg_file=dict(argstr='--xfm %s', extensions=None, mandatory=True, xor=('reg_file', 'lta_file', 'lta_inv_file', 'fsl_reg_file', 'xfm_reg_file', 'reg_header', 'mni_152_reg', 'subject')))
```

## Next Steps


---

*Source: test_auto_ApplyVolTransform.py:6 | Complexity: Beginner | Last updated: 2026-05-18*