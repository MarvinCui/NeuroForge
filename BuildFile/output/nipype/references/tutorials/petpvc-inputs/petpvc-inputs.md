# How To: Petpvc Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test PETPVC inputs

## Prerequisites

**Required Modules:**
- `petpvc`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(alpha=dict(argstr='-a %.4f', usedefault=True), args=dict(argstr='%s'), debug=dict(argstr='-d', usedefault=True), environ=dict(nohash=True, usedefault=True), fwhm_x=dict(argstr='-x %.4f', mandatory=True), fwhm_y=dict(argstr='-y %.4f', mandatory=True), fwhm_z=dict(argstr='-z %.4f', mandatory=True), in_file=dict(argstr='-i %s', extensions=None, mandatory=True), mask_file=dict(argstr='-m %s', extensions=None, mandatory=True), n_deconv=dict(argstr='-k %d', usedefault=True), n_iter=dict(argstr='-n %d', usedefault=True), out_file=dict(argstr='-o %s', extensions=None, genfile=True, hash_files=False), pvc=dict(argstr='-p %s', mandatory=True), stop_crit=dict(argstr='-s %.4f', usedefault=True))
```


## Complete Example

```python
# Workflow
input_map = dict(alpha=dict(argstr='-a %.4f', usedefault=True), args=dict(argstr='%s'), debug=dict(argstr='-d', usedefault=True), environ=dict(nohash=True, usedefault=True), fwhm_x=dict(argstr='-x %.4f', mandatory=True), fwhm_y=dict(argstr='-y %.4f', mandatory=True), fwhm_z=dict(argstr='-z %.4f', mandatory=True), in_file=dict(argstr='-i %s', extensions=None, mandatory=True), mask_file=dict(argstr='-m %s', extensions=None, mandatory=True), n_deconv=dict(argstr='-k %d', usedefault=True), n_iter=dict(argstr='-n %d', usedefault=True), out_file=dict(argstr='-o %s', extensions=None, genfile=True, hash_files=False), pvc=dict(argstr='-p %s', mandatory=True), stop_crit=dict(argstr='-s %.4f', usedefault=True))
```

## Next Steps


---

*Source: test_auto_PETPVC.py:6 | Complexity: Beginner | Last updated: 2026-05-18*