# How To: Gtmpvc Outputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test GTMPVC outputs

## Prerequisites

**Required Modules:**
- `petsurfer`


## Step-by-Step Guide

### Step 1: Assign output_map = dict(...)

```python
output_map = dict(eres=dict(extensions=None), gtm_file=dict(extensions=None), gtm_stats=dict(extensions=None), hb_dat=dict(extensions=None), hb_nifti=dict(extensions=None), input_file=dict(extensions=None), mgx_ctxgm=dict(extensions=None), mgx_gm=dict(extensions=None), mgx_subctxgm=dict(extensions=None), nopvc_file=dict(extensions=None), opt_params=dict(extensions=None), pvc_dir=dict(), rbv=dict(extensions=None), ref_file=dict(extensions=None), reg_anat2pet=dict(extensions=None), reg_anat2rbvpet=dict(extensions=None), reg_pet2anat=dict(extensions=None), reg_rbvpet2anat=dict(extensions=None), seg=dict(extensions=None), seg_ctab=dict(extensions=None), tissue_fraction=dict(extensions=None), tissue_fraction_psf=dict(extensions=None), yhat=dict(extensions=None), yhat0=dict(extensions=None), yhat_full_fov=dict(extensions=None), yhat_with_noise=dict(extensions=None))
```


## Complete Example

```python
# Workflow
output_map = dict(eres=dict(extensions=None), gtm_file=dict(extensions=None), gtm_stats=dict(extensions=None), hb_dat=dict(extensions=None), hb_nifti=dict(extensions=None), input_file=dict(extensions=None), mgx_ctxgm=dict(extensions=None), mgx_gm=dict(extensions=None), mgx_subctxgm=dict(extensions=None), nopvc_file=dict(extensions=None), opt_params=dict(extensions=None), pvc_dir=dict(), rbv=dict(extensions=None), ref_file=dict(extensions=None), reg_anat2pet=dict(extensions=None), reg_anat2rbvpet=dict(extensions=None), reg_pet2anat=dict(extensions=None), reg_rbvpet2anat=dict(extensions=None), seg=dict(extensions=None), seg_ctab=dict(extensions=None), tissue_fraction=dict(extensions=None), tissue_fraction_psf=dict(extensions=None), yhat=dict(extensions=None), yhat0=dict(extensions=None), yhat_full_fov=dict(extensions=None), yhat_with_noise=dict(extensions=None))
```

## Next Steps


---

*Source: test_auto_GTMPVC.py:209 | Complexity: Beginner | Last updated: 2026-05-18*