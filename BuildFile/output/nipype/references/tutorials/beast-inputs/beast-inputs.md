# How To: Beast Inputs

**Difficulty**: Intermediate
**Estimated Time**: 5 minutes
**Tags**: mock

## Overview

Instantiate dict: test Beast inputs

## Prerequisites

**Required Modules:**
- `minc`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(abspath=dict(argstr='-abspath', usedefault=True), args=dict(argstr='%s'), clobber=dict(argstr='-clobber', usedefault=True), confidence_level_alpha=dict(argstr='-alpha %s', usedefault=True), configuration_file=dict(argstr='-configuration %s', extensions=None), environ=dict(nohash=True, usedefault=True), fill_holes=dict(argstr='-fill'), flip_images=dict(argstr='-flip'), input_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), library_dir=dict(argstr='%s', mandatory=True, position=-3), load_moments=dict(argstr='-load_moments'), median_filter=dict(argstr='-median'), nlm_filter=dict(argstr='-nlm_filter'), number_selected_images=dict(argstr='-selection_num %s', usedefault=True), output_file=dict(argstr='%s', extensions=None, hash_files=False, name_source=['input_file'], name_template='%s_beast_mask.mnc', position=-1), patch_size=dict(argstr='-patch_size %s', usedefault=True), probability_map=dict(argstr='-probability'), same_resolution=dict(argstr='-same_resolution'), search_area=dict(argstr='-search_area %s', usedefault=True), smoothness_factor_beta=dict(argstr='-beta %s', usedefault=True), threshold_patch_selection=dict(argstr='-threshold %s', usedefault=True), voxel_size=dict(argstr='-voxel_size %s', usedefault=True))
```


## Complete Example

```python
# Workflow
input_map = dict(abspath=dict(argstr='-abspath', usedefault=True), args=dict(argstr='%s'), clobber=dict(argstr='-clobber', usedefault=True), confidence_level_alpha=dict(argstr='-alpha %s', usedefault=True), configuration_file=dict(argstr='-configuration %s', extensions=None), environ=dict(nohash=True, usedefault=True), fill_holes=dict(argstr='-fill'), flip_images=dict(argstr='-flip'), input_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), library_dir=dict(argstr='%s', mandatory=True, position=-3), load_moments=dict(argstr='-load_moments'), median_filter=dict(argstr='-median'), nlm_filter=dict(argstr='-nlm_filter'), number_selected_images=dict(argstr='-selection_num %s', usedefault=True), output_file=dict(argstr='%s', extensions=None, hash_files=False, name_source=['input_file'], name_template='%s_beast_mask.mnc', position=-1), patch_size=dict(argstr='-patch_size %s', usedefault=True), probability_map=dict(argstr='-probability'), same_resolution=dict(argstr='-same_resolution'), search_area=dict(argstr='-search_area %s', usedefault=True), smoothness_factor_beta=dict(argstr='-beta %s', usedefault=True), threshold_patch_selection=dict(argstr='-threshold %s', usedefault=True), voxel_size=dict(argstr='-voxel_size %s', usedefault=True))
```

## Next Steps


---

*Source: test_auto_Beast.py:6 | Complexity: Intermediate | Last updated: 2026-05-18*