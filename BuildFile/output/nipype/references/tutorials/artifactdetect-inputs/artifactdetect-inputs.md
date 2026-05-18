# How To: Artifactdetect Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test ArtifactDetect inputs

## Prerequisites

**Required Modules:**
- `rapidart`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(bound_by_brainmask=dict(usedefault=True), global_threshold=dict(usedefault=True), intersect_mask=dict(usedefault=True), mask_file=dict(extensions=None), mask_threshold=dict(), mask_type=dict(mandatory=True), norm_threshold=dict(mandatory=True, xor=['rotation_threshold', 'translation_threshold']), parameter_source=dict(mandatory=True), plot_type=dict(usedefault=True), realigned_files=dict(mandatory=True), realignment_parameters=dict(mandatory=True), rotation_threshold=dict(mandatory=True, xor=['norm_threshold']), save_plot=dict(usedefault=True), translation_threshold=dict(mandatory=True, xor=['norm_threshold']), use_differences=dict(usedefault=True), use_norm=dict(requires=['norm_threshold'], usedefault=True), zintensity_threshold=dict(mandatory=True))
```


## Complete Example

```python
# Workflow
input_map = dict(bound_by_brainmask=dict(usedefault=True), global_threshold=dict(usedefault=True), intersect_mask=dict(usedefault=True), mask_file=dict(extensions=None), mask_threshold=dict(), mask_type=dict(mandatory=True), norm_threshold=dict(mandatory=True, xor=['rotation_threshold', 'translation_threshold']), parameter_source=dict(mandatory=True), plot_type=dict(usedefault=True), realigned_files=dict(mandatory=True), realignment_parameters=dict(mandatory=True), rotation_threshold=dict(mandatory=True, xor=['norm_threshold']), save_plot=dict(usedefault=True), translation_threshold=dict(mandatory=True, xor=['norm_threshold']), use_differences=dict(usedefault=True), use_norm=dict(requires=['norm_threshold'], usedefault=True), zintensity_threshold=dict(mandatory=True))
```

## Next Steps


---

*Source: test_auto_ArtifactDetect.py:6 | Complexity: Beginner | Last updated: 2026-05-18*