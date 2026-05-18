# How To: Creatematrix Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test CreateMatrix inputs

## Prerequisites

**Required Modules:**
- `cmtk`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(count_region_intersections=dict(usedefault=True), out_endpoint_array_name=dict(extensions=None, genfile=True), out_fiber_length_std_matrix_mat_file=dict(extensions=None, genfile=True), out_intersection_matrix_mat_file=dict(extensions=None, genfile=True), out_matrix_file=dict(extensions=None, genfile=True), out_matrix_mat_file=dict(extensions=None, usedefault=True), out_mean_fiber_length_matrix_mat_file=dict(extensions=None, genfile=True), out_median_fiber_length_matrix_mat_file=dict(extensions=None, genfile=True), resolution_network_file=dict(extensions=None, mandatory=True), roi_file=dict(extensions=None, mandatory=True), tract_file=dict(extensions=None, mandatory=True))
```


## Complete Example

```python
# Workflow
input_map = dict(count_region_intersections=dict(usedefault=True), out_endpoint_array_name=dict(extensions=None, genfile=True), out_fiber_length_std_matrix_mat_file=dict(extensions=None, genfile=True), out_intersection_matrix_mat_file=dict(extensions=None, genfile=True), out_matrix_file=dict(extensions=None, genfile=True), out_matrix_mat_file=dict(extensions=None, usedefault=True), out_mean_fiber_length_matrix_mat_file=dict(extensions=None, genfile=True), out_median_fiber_length_matrix_mat_file=dict(extensions=None, genfile=True), resolution_network_file=dict(extensions=None, mandatory=True), roi_file=dict(extensions=None, mandatory=True), tract_file=dict(extensions=None, mandatory=True))
```

## Next Steps


---

*Source: test_auto_CreateMatrix.py:6 | Complexity: Beginner | Last updated: 2026-05-18*