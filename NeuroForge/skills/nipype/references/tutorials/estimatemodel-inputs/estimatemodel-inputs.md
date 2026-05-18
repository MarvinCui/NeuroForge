# How To: Estimatemodel Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test EstimateModel inputs

## Prerequisites

**Required Modules:**
- `model`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(estimation_method=dict(field='method', mandatory=True), flags=dict(), matlab_cmd=dict(), mfile=dict(usedefault=True), paths=dict(), spm_mat_file=dict(copyfile=True, extensions=None, field='spmmat', mandatory=True), use_mcr=dict(), use_v8struct=dict(min_ver='8', usedefault=True), write_residuals=dict(field='write_residuals'))
```


## Complete Example

```python
# Workflow
input_map = dict(estimation_method=dict(field='method', mandatory=True), flags=dict(), matlab_cmd=dict(), mfile=dict(usedefault=True), paths=dict(), spm_mat_file=dict(copyfile=True, extensions=None, field='spmmat', mandatory=True), use_mcr=dict(), use_v8struct=dict(min_ver='8', usedefault=True), write_residuals=dict(field='write_residuals'))
```

## Next Steps


---

*Source: test_auto_EstimateModel.py:6 | Complexity: Beginner | Last updated: 2026-05-18*