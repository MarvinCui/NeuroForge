# How To: Glm Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test GLM inputs

## Prerequisites

**Required Modules:**
- `model`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), contrasts=dict(argstr='-c %s', extensions=None), dat_norm=dict(argstr='--dat_norm'), demean=dict(argstr='--demean'), des_norm=dict(argstr='--des_norm'), design=dict(argstr='-d %s', extensions=None, mandatory=True, position=2), dof=dict(argstr='--dof=%d'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-i %s', extensions=None, mandatory=True, position=1), mask=dict(argstr='-m %s', extensions=None), out_cope=dict(argstr='--out_cope=%s', extensions=None), out_data_name=dict(argstr='--out_data=%s', extensions=None), out_f_name=dict(argstr='--out_f=%s', extensions=None), out_file=dict(argstr='-o %s', extensions=None, keep_extension=True, name_source='in_file', name_template='%s_glm', position=3), out_p_name=dict(argstr='--out_p=%s', extensions=None), out_pf_name=dict(argstr='--out_pf=%s', extensions=None), out_res_name=dict(argstr='--out_res=%s', extensions=None), out_sigsq_name=dict(argstr='--out_sigsq=%s', extensions=None), out_t_name=dict(argstr='--out_t=%s', extensions=None), out_varcb_name=dict(argstr='--out_varcb=%s', extensions=None), out_vnscales_name=dict(argstr='--out_vnscales=%s', extensions=None), out_z_name=dict(argstr='--out_z=%s', extensions=None), output_type=dict(), var_norm=dict(argstr='--vn'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), contrasts=dict(argstr='-c %s', extensions=None), dat_norm=dict(argstr='--dat_norm'), demean=dict(argstr='--demean'), des_norm=dict(argstr='--des_norm'), design=dict(argstr='-d %s', extensions=None, mandatory=True, position=2), dof=dict(argstr='--dof=%d'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-i %s', extensions=None, mandatory=True, position=1), mask=dict(argstr='-m %s', extensions=None), out_cope=dict(argstr='--out_cope=%s', extensions=None), out_data_name=dict(argstr='--out_data=%s', extensions=None), out_f_name=dict(argstr='--out_f=%s', extensions=None), out_file=dict(argstr='-o %s', extensions=None, keep_extension=True, name_source='in_file', name_template='%s_glm', position=3), out_p_name=dict(argstr='--out_p=%s', extensions=None), out_pf_name=dict(argstr='--out_pf=%s', extensions=None), out_res_name=dict(argstr='--out_res=%s', extensions=None), out_sigsq_name=dict(argstr='--out_sigsq=%s', extensions=None), out_t_name=dict(argstr='--out_t=%s', extensions=None), out_varcb_name=dict(argstr='--out_varcb=%s', extensions=None), out_vnscales_name=dict(argstr='--out_vnscales=%s', extensions=None), out_z_name=dict(argstr='--out_z=%s', extensions=None), output_type=dict(), var_norm=dict(argstr='--vn'))
```

## Next Steps


---

*Source: test_auto_GLM.py:6 | Complexity: Beginner | Last updated: 2026-05-18*