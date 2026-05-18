# How To: Fslroi

**Difficulty**: Beginner
**Estimated Time**: 5 minutes
**Tags**: pytest

## Overview

Instantiate ExtractROI: test fslroi

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `numpy`
- `pytest`
- `nipype.interfaces.fsl.utils`
- `nipype.interfaces.fsl`
- `nipype.testing.fixtures`

**Setup Required:**
```python
# Fixtures: create_files_in_directory_plus_output_type
```

## Step-by-Step Guide

### Step 1: Assign roi2 = fsl.ExtractROI(...)

```python
roi2 = fsl.ExtractROI(in_file=filelist[0], roi_file='foo2_roi.nii', t_min=20, t_size=40, x_min=3, x_size=30, y_min=40, y_size=10, z_min=5, z_size=20)
```


## Complete Example

```python
# Setup
# Fixtures: create_files_in_directory_plus_output_type

# Workflow
roi2 = fsl.ExtractROI(in_file=filelist[0], roi_file='foo2_roi.nii', t_min=20, t_size=40, x_min=3, x_size=30, y_min=40, y_size=10, z_min=5, z_size=20)
```

## Next Steps


---

*Source: test_utils.py:36 | Complexity: Beginner | Last updated: 2026-05-18*