# How To: Netcorr Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test NetCorr inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), fish_z=dict(argstr='-fish_z'), ignore_LT=dict(argstr='-ignore_LT'), in_file=dict(argstr='-inset %s', extensions=None, mandatory=True), in_rois=dict(argstr='-in_rois %s', extensions=None, mandatory=True), mask=dict(argstr='-mask %s', extensions=None), nifti=dict(argstr='-nifti'), num_threads=dict(nohash=True, usedefault=True), out_file=dict(argstr='-prefix %s', extensions=None, name_source='in_file', name_template='%s_netcorr', position=1), output_mask_nonnull=dict(argstr='-output_mask_nonnull'), outputtype=dict(), part_corr=dict(argstr='-part_corr'), push_thru_many_zeros=dict(argstr='-push_thru_many_zeros'), ts_indiv=dict(argstr='-ts_indiv'), ts_label=dict(argstr='-ts_label'), ts_out=dict(argstr='-ts_out'), ts_wb_Z=dict(argstr='-ts_wb_Z'), ts_wb_corr=dict(argstr='-ts_wb_corr'), ts_wb_strlabel=dict(argstr='-ts_wb_strlabel'), weight_ts=dict(argstr='-weight_ts %s', extensions=None))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), fish_z=dict(argstr='-fish_z'), ignore_LT=dict(argstr='-ignore_LT'), in_file=dict(argstr='-inset %s', extensions=None, mandatory=True), in_rois=dict(argstr='-in_rois %s', extensions=None, mandatory=True), mask=dict(argstr='-mask %s', extensions=None), nifti=dict(argstr='-nifti'), num_threads=dict(nohash=True, usedefault=True), out_file=dict(argstr='-prefix %s', extensions=None, name_source='in_file', name_template='%s_netcorr', position=1), output_mask_nonnull=dict(argstr='-output_mask_nonnull'), outputtype=dict(), part_corr=dict(argstr='-part_corr'), push_thru_many_zeros=dict(argstr='-push_thru_many_zeros'), ts_indiv=dict(argstr='-ts_indiv'), ts_label=dict(argstr='-ts_label'), ts_out=dict(argstr='-ts_out'), ts_wb_Z=dict(argstr='-ts_wb_Z'), ts_wb_corr=dict(argstr='-ts_wb_corr'), ts_wb_strlabel=dict(argstr='-ts_wb_strlabel'), weight_ts=dict(argstr='-weight_ts %s', extensions=None))
```

## Next Steps


---

*Source: test_auto_NetCorr.py:6 | Complexity: Beginner | Last updated: 2026-05-18*