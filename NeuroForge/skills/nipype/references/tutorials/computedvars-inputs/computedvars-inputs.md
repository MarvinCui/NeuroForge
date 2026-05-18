# How To: Computedvars Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test ComputeDVARS inputs

## Prerequisites

**Required Modules:**
- `confounds`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(figdpi=dict(usedefault=True), figformat=dict(usedefault=True), figsize=dict(usedefault=True), in_file=dict(extensions=None, mandatory=True), in_mask=dict(extensions=None, mandatory=True), intensity_normalization=dict(usedefault=True), remove_zerovariance=dict(usedefault=True), save_all=dict(usedefault=True), save_nstd=dict(usedefault=True), save_plot=dict(usedefault=True), save_std=dict(usedefault=True), save_vxstd=dict(usedefault=True), series_tr=dict(), variance_tol=dict(usedefault=True))
```


## Complete Example

```python
# Workflow
input_map = dict(figdpi=dict(usedefault=True), figformat=dict(usedefault=True), figsize=dict(usedefault=True), in_file=dict(extensions=None, mandatory=True), in_mask=dict(extensions=None, mandatory=True), intensity_normalization=dict(usedefault=True), remove_zerovariance=dict(usedefault=True), save_all=dict(usedefault=True), save_nstd=dict(usedefault=True), save_plot=dict(usedefault=True), save_std=dict(usedefault=True), save_vxstd=dict(usedefault=True), series_tr=dict(), variance_tol=dict(usedefault=True))
```

## Next Steps


---

*Source: test_auto_ComputeDVARS.py:6 | Complexity: Beginner | Last updated: 2026-05-18*