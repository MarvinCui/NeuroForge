# How To: Estimatecontrast Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test EstimateContrast inputs

## Prerequisites

**Required Modules:**
- `model`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(beta_images=dict(copyfile=False, mandatory=True), contrasts=dict(mandatory=True), group_contrast=dict(xor=['use_derivs']), matlab_cmd=dict(), mfile=dict(usedefault=True), paths=dict(), residual_image=dict(copyfile=False, extensions=None, mandatory=True), spm_mat_file=dict(copyfile=True, extensions=None, field='spmmat', mandatory=True), use_derivs=dict(xor=['group_contrast']), use_mcr=dict(), use_v8struct=dict(min_ver='8', usedefault=True))
```


## Complete Example

```python
# Workflow
input_map = dict(beta_images=dict(copyfile=False, mandatory=True), contrasts=dict(mandatory=True), group_contrast=dict(xor=['use_derivs']), matlab_cmd=dict(), mfile=dict(usedefault=True), paths=dict(), residual_image=dict(copyfile=False, extensions=None, mandatory=True), spm_mat_file=dict(copyfile=True, extensions=None, field='spmmat', mandatory=True), use_derivs=dict(xor=['group_contrast']), use_mcr=dict(), use_v8struct=dict(min_ver='8', usedefault=True))
```

## Next Steps


---

*Source: test_auto_EstimateContrast.py:6 | Complexity: Beginner | Last updated: 2026-05-18*