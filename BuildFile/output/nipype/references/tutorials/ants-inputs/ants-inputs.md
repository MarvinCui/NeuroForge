# How To: Ants Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test ANTS inputs

## Prerequisites

**Required Modules:**
- `registration`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(affine_gradient_descent_option=dict(argstr='%s'), args=dict(argstr='%s'), delta_time=dict(requires=['number_of_time_steps']), dimension=dict(argstr='%d', position=1), environ=dict(nohash=True, usedefault=True), fixed_image=dict(mandatory=True), gradient_step_length=dict(requires=['transformation_model']), metric=dict(mandatory=True), metric_weight=dict(mandatory=True, requires=['metric'], usedefault=True), mi_option=dict(argstr='--MI-option %s', sep='x'), moving_image=dict(argstr='%s', mandatory=True), num_threads=dict(nohash=True, usedefault=True), number_of_affine_iterations=dict(argstr='--number-of-affine-iterations %s', sep='x'), number_of_iterations=dict(argstr='--number-of-iterations %s', sep='x'), number_of_time_steps=dict(requires=['gradient_step_length']), output_transform_prefix=dict(argstr='--output-naming %s', mandatory=True, usedefault=True), radius=dict(mandatory=True, requires=['metric']), regularization=dict(argstr='%s'), regularization_deformation_field_sigma=dict(requires=['regularization']), regularization_gradient_field_sigma=dict(requires=['regularization']), smoothing_sigmas=dict(argstr='--gaussian-smoothing-sigmas %s', sep='x'), subsampling_factors=dict(argstr='--subsampling-factors %s', sep='x'), symmetry_type=dict(requires=['delta_time']), transformation_model=dict(argstr='%s', mandatory=True), use_histogram_matching=dict(argstr='%s', usedefault=True))
```


## Complete Example

```python
# Workflow
input_map = dict(affine_gradient_descent_option=dict(argstr='%s'), args=dict(argstr='%s'), delta_time=dict(requires=['number_of_time_steps']), dimension=dict(argstr='%d', position=1), environ=dict(nohash=True, usedefault=True), fixed_image=dict(mandatory=True), gradient_step_length=dict(requires=['transformation_model']), metric=dict(mandatory=True), metric_weight=dict(mandatory=True, requires=['metric'], usedefault=True), mi_option=dict(argstr='--MI-option %s', sep='x'), moving_image=dict(argstr='%s', mandatory=True), num_threads=dict(nohash=True, usedefault=True), number_of_affine_iterations=dict(argstr='--number-of-affine-iterations %s', sep='x'), number_of_iterations=dict(argstr='--number-of-iterations %s', sep='x'), number_of_time_steps=dict(requires=['gradient_step_length']), output_transform_prefix=dict(argstr='--output-naming %s', mandatory=True, usedefault=True), radius=dict(mandatory=True, requires=['metric']), regularization=dict(argstr='%s'), regularization_deformation_field_sigma=dict(requires=['regularization']), regularization_gradient_field_sigma=dict(requires=['regularization']), smoothing_sigmas=dict(argstr='--gaussian-smoothing-sigmas %s', sep='x'), subsampling_factors=dict(argstr='--subsampling-factors %s', sep='x'), symmetry_type=dict(requires=['delta_time']), transformation_model=dict(argstr='%s', mandatory=True), use_histogram_matching=dict(argstr='%s', usedefault=True))
```

## Next Steps


---

*Source: test_auto_ANTS.py:6 | Complexity: Beginner | Last updated: 2026-05-18*