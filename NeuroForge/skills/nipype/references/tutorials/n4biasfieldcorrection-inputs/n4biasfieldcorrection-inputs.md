# How To: N4Biasfieldcorrection Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test N4BiasFieldCorrection inputs

## Prerequisites

**Required Modules:**
- `segmentation`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), bias_image=dict(extensions=None, hash_files=False), bspline_fitting_distance=dict(argstr='--bspline-fitting %s'), bspline_order=dict(requires=['bspline_fitting_distance']), convergence_threshold=dict(requires=['n_iterations']), copy_header=dict(mandatory=True, usedefault=True), dimension=dict(argstr='-d %d', usedefault=True), environ=dict(nohash=True, usedefault=True), histogram_sharpening=dict(argstr='--histogram-sharpening [%g,%g,%d]'), input_image=dict(argstr='--input-image %s', extensions=None, mandatory=True), mask_image=dict(argstr='--mask-image %s', extensions=None), n_iterations=dict(argstr='--convergence %s'), num_threads=dict(nohash=True, usedefault=True), output_image=dict(argstr='--output %s', hash_files=False, keep_extension=True, name_source=['input_image'], name_template='%s_corrected'), rescale_intensities=dict(argstr='-r', min_ver='2.1.0', usedefault=True), save_bias=dict(mandatory=True, usedefault=True, xor=['bias_image']), shrink_factor=dict(argstr='--shrink-factor %d'), weight_image=dict(argstr='--weight-image %s', extensions=None))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), bias_image=dict(extensions=None, hash_files=False), bspline_fitting_distance=dict(argstr='--bspline-fitting %s'), bspline_order=dict(requires=['bspline_fitting_distance']), convergence_threshold=dict(requires=['n_iterations']), copy_header=dict(mandatory=True, usedefault=True), dimension=dict(argstr='-d %d', usedefault=True), environ=dict(nohash=True, usedefault=True), histogram_sharpening=dict(argstr='--histogram-sharpening [%g,%g,%d]'), input_image=dict(argstr='--input-image %s', extensions=None, mandatory=True), mask_image=dict(argstr='--mask-image %s', extensions=None), n_iterations=dict(argstr='--convergence %s'), num_threads=dict(nohash=True, usedefault=True), output_image=dict(argstr='--output %s', hash_files=False, keep_extension=True, name_source=['input_image'], name_template='%s_corrected'), rescale_intensities=dict(argstr='-r', min_ver='2.1.0', usedefault=True), save_bias=dict(mandatory=True, usedefault=True, xor=['bias_image']), shrink_factor=dict(argstr='--shrink-factor %d'), weight_image=dict(argstr='--weight-image %s', extensions=None))
```

## Next Steps


---

*Source: test_auto_N4BiasFieldCorrection.py:6 | Complexity: Beginner | Last updated: 2026-05-18*