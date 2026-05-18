# How To: Creatematrix Outputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test CreateMatrix outputs

## Prerequisites

**Required Modules:**
- `cmtk`


## Step-by-Step Guide

### Step 1: Assign output_map = dict(...)

```python
output_map = dict(endpoint_file=dict(extensions=None), endpoint_file_mm=dict(extensions=None), fiber_label_file=dict(extensions=None), fiber_labels_noorphans=dict(extensions=None), fiber_length_file=dict(extensions=None), fiber_length_std_matrix_mat_file=dict(extensions=None), filtered_tractographies=dict(), filtered_tractography=dict(extensions=None), filtered_tractography_by_intersections=dict(extensions=None), intersection_matrix_file=dict(extensions=None), intersection_matrix_mat_file=dict(extensions=None), matlab_matrix_files=dict(), matrix_file=dict(extensions=None), matrix_files=dict(), matrix_mat_file=dict(extensions=None), mean_fiber_length_matrix_mat_file=dict(extensions=None), median_fiber_length_matrix_mat_file=dict(extensions=None), stats_file=dict(extensions=None))
```


## Complete Example

```python
# Workflow
output_map = dict(endpoint_file=dict(extensions=None), endpoint_file_mm=dict(extensions=None), fiber_label_file=dict(extensions=None), fiber_labels_noorphans=dict(extensions=None), fiber_length_file=dict(extensions=None), fiber_length_std_matrix_mat_file=dict(extensions=None), filtered_tractographies=dict(), filtered_tractography=dict(extensions=None), filtered_tractography_by_intersections=dict(extensions=None), intersection_matrix_file=dict(extensions=None), intersection_matrix_mat_file=dict(extensions=None), matlab_matrix_files=dict(), matrix_file=dict(extensions=None), matrix_files=dict(), matrix_mat_file=dict(extensions=None), mean_fiber_length_matrix_mat_file=dict(extensions=None), median_fiber_length_matrix_mat_file=dict(extensions=None), stats_file=dict(extensions=None))
```

## Next Steps


---

*Source: test_auto_CreateMatrix.py:59 | Complexity: Beginner | Last updated: 2026-05-18*