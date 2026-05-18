# How To: Simulatemultitensor Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test SimulateMultiTensor inputs

## Prerequisites

**Required Modules:**
- `simulate`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(baseline=dict(extensions=None, mandatory=True), bvalues=dict(usedefault=True), diff_iso=dict(usedefault=True), diff_sf=dict(usedefault=True), gradients=dict(extensions=None), in_bval=dict(extensions=None), in_bvec=dict(extensions=None), in_dirs=dict(mandatory=True), in_frac=dict(mandatory=True), in_mask=dict(extensions=None), in_vfms=dict(mandatory=True), n_proc=dict(usedefault=True), num_dirs=dict(usedefault=True), out_bval=dict(extensions=None, usedefault=True), out_bvec=dict(extensions=None, usedefault=True), out_file=dict(extensions=None, usedefault=True), out_mask=dict(extensions=None, usedefault=True), snr=dict(usedefault=True))
```


## Complete Example

```python
# Workflow
input_map = dict(baseline=dict(extensions=None, mandatory=True), bvalues=dict(usedefault=True), diff_iso=dict(usedefault=True), diff_sf=dict(usedefault=True), gradients=dict(extensions=None), in_bval=dict(extensions=None), in_bvec=dict(extensions=None), in_dirs=dict(mandatory=True), in_frac=dict(mandatory=True), in_mask=dict(extensions=None), in_vfms=dict(mandatory=True), n_proc=dict(usedefault=True), num_dirs=dict(usedefault=True), out_bval=dict(extensions=None, usedefault=True), out_bvec=dict(extensions=None, usedefault=True), out_file=dict(extensions=None, usedefault=True), out_mask=dict(extensions=None, usedefault=True), snr=dict(usedefault=True))
```

## Next Steps


---

*Source: test_auto_SimulateMultiTensor.py:6 | Complexity: Beginner | Last updated: 2026-05-18*