# How To: Dwipreproc Outputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test DWIPreproc outputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign output_map = dict(...)

```python
output_map = dict(out_file=dict(argstr='%s', extensions=None), out_fsl_bval=dict(argstr='%s', extensions=None, usedefault=True), out_fsl_bvec=dict(argstr='%s', extensions=None, usedefault=True), out_grad_mrtrix=dict(argstr='%s', extensions=None, usedefault=True))
```


## Complete Example

```python
# Workflow
output_map = dict(out_file=dict(argstr='%s', extensions=None), out_fsl_bval=dict(argstr='%s', extensions=None, usedefault=True), out_fsl_bvec=dict(argstr='%s', extensions=None, usedefault=True), out_grad_mrtrix=dict(argstr='%s', extensions=None, usedefault=True))
```

## Next Steps


---

*Source: test_auto_DWIPreproc.py:115 | Complexity: Beginner | Last updated: 2026-05-18*