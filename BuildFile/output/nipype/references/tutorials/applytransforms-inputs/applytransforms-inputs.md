# How To: Applytransforms Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test ApplyTransforms inputs

## Prerequisites

**Required Modules:**
- `resampling`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), default_value=dict(argstr='--default-value %g', usedefault=True), dimension=dict(argstr='--dimensionality %d'), environ=dict(nohash=True, usedefault=True), float=dict(argstr='--float %d', usedefault=True), input_image=dict(argstr='--input %s', extensions=None, mandatory=True), input_image_type=dict(argstr='--input-image-type %d'), interpolation=dict(argstr='%s', usedefault=True), interpolation_parameters=dict(), invert_transform_flags=dict(), num_threads=dict(nohash=True, usedefault=True), out_postfix=dict(usedefault=True), output_image=dict(argstr='--output %s', genfile=True, hash_files=False), print_out_composite_warp_file=dict(requires=['output_image']), reference_image=dict(argstr='--reference-image %s', extensions=None, mandatory=True), transforms=dict(argstr='%s', mandatory=True))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), default_value=dict(argstr='--default-value %g', usedefault=True), dimension=dict(argstr='--dimensionality %d'), environ=dict(nohash=True, usedefault=True), float=dict(argstr='--float %d', usedefault=True), input_image=dict(argstr='--input %s', extensions=None, mandatory=True), input_image_type=dict(argstr='--input-image-type %d'), interpolation=dict(argstr='%s', usedefault=True), interpolation_parameters=dict(), invert_transform_flags=dict(), num_threads=dict(nohash=True, usedefault=True), out_postfix=dict(usedefault=True), output_image=dict(argstr='--output %s', genfile=True, hash_files=False), print_out_composite_warp_file=dict(requires=['output_image']), reference_image=dict(argstr='--reference-image %s', extensions=None, mandatory=True), transforms=dict(argstr='%s', mandatory=True))
```

## Next Steps


---

*Source: test_auto_ApplyTransforms.py:6 | Complexity: Beginner | Last updated: 2026-05-18*