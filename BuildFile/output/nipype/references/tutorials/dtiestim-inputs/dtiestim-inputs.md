# How To: Dtiestim Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test dtiestim inputs

## Prerequisites

**Required Modules:**
- `diffusion`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(B0=dict(argstr='--B0 %s', hash_files=False), B0_mask_output=dict(argstr='--B0_mask_output %s', hash_files=False), DTI_double=dict(argstr='--DTI_double '), args=dict(argstr='%s'), bad_region_mask=dict(argstr='--bad_region_mask %s', extensions=None), brain_mask=dict(argstr='--brain_mask %s', extensions=None), correction=dict(argstr='--correction %s'), defaultTensor=dict(argstr='--defaultTensor %s', sep=','), dwi_image=dict(argstr='--dwi_image %s', extensions=None), environ=dict(nohash=True, usedefault=True), idwi=dict(argstr='--idwi %s', hash_files=False), method=dict(argstr='--method %s'), shiftNeg=dict(argstr='--shiftNeg '), shiftNegCoeff=dict(argstr='--shiftNegCoeff %f'), sigma=dict(argstr='--sigma %f'), step=dict(argstr='--step %f'), tensor_output=dict(argstr='--tensor_output %s', hash_files=False), threshold=dict(argstr='--threshold %d'), verbose=dict(argstr='--verbose '), weight_iterations=dict(argstr='--weight_iterations %d'))
```


## Complete Example

```python
# Workflow
input_map = dict(B0=dict(argstr='--B0 %s', hash_files=False), B0_mask_output=dict(argstr='--B0_mask_output %s', hash_files=False), DTI_double=dict(argstr='--DTI_double '), args=dict(argstr='%s'), bad_region_mask=dict(argstr='--bad_region_mask %s', extensions=None), brain_mask=dict(argstr='--brain_mask %s', extensions=None), correction=dict(argstr='--correction %s'), defaultTensor=dict(argstr='--defaultTensor %s', sep=','), dwi_image=dict(argstr='--dwi_image %s', extensions=None), environ=dict(nohash=True, usedefault=True), idwi=dict(argstr='--idwi %s', hash_files=False), method=dict(argstr='--method %s'), shiftNeg=dict(argstr='--shiftNeg '), shiftNegCoeff=dict(argstr='--shiftNegCoeff %f'), sigma=dict(argstr='--sigma %f'), step=dict(argstr='--step %f'), tensor_output=dict(argstr='--tensor_output %s', hash_files=False), threshold=dict(argstr='--threshold %d'), verbose=dict(argstr='--verbose '), weight_iterations=dict(argstr='--weight_iterations %d'))
```

## Next Steps


---

*Source: test_auto_dtiestim.py:6 | Complexity: Beginner | Last updated: 2026-05-18*