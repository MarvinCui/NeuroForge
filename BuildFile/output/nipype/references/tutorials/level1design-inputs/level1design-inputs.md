# How To: Level1Design Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Level1Design inputs

## Prerequisites

**Required Modules:**
- `model`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(bases=dict(field='bases', mandatory=True), factor_info=dict(field='fact'), flags=dict(), global_intensity_normalization=dict(field='global'), interscan_interval=dict(field='timing.RT', mandatory=True), mask_image=dict(extensions=None, field='mask'), mask_threshold=dict(usedefault=True), matlab_cmd=dict(), mfile=dict(usedefault=True), microtime_onset=dict(field='timing.fmri_t0'), microtime_resolution=dict(field='timing.fmri_t'), model_serial_correlations=dict(field='cvi'), paths=dict(), session_info=dict(field='sess', mandatory=True), spm_mat_dir=dict(field='dir'), timing_units=dict(field='timing.units', mandatory=True), use_mcr=dict(), use_v8struct=dict(min_ver='8', usedefault=True), volterra_expansion_order=dict(field='volt'))
```


## Complete Example

```python
# Workflow
input_map = dict(bases=dict(field='bases', mandatory=True), factor_info=dict(field='fact'), flags=dict(), global_intensity_normalization=dict(field='global'), interscan_interval=dict(field='timing.RT', mandatory=True), mask_image=dict(extensions=None, field='mask'), mask_threshold=dict(usedefault=True), matlab_cmd=dict(), mfile=dict(usedefault=True), microtime_onset=dict(field='timing.fmri_t0'), microtime_resolution=dict(field='timing.fmri_t'), model_serial_correlations=dict(field='cvi'), paths=dict(), session_info=dict(field='sess', mandatory=True), spm_mat_dir=dict(field='dir'), timing_units=dict(field='timing.units', mandatory=True), use_mcr=dict(), use_v8struct=dict(min_ver='8', usedefault=True), volterra_expansion_order=dict(field='volt'))
```

## Next Steps


---

*Source: test_auto_Level1Design.py:6 | Complexity: Beginner | Last updated: 2026-05-18*