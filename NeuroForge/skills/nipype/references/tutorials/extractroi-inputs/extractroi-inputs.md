# How To: Extractroi Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test ExtractROI inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), crop_list=dict(argstr='%s', position=2, xor=['x_min', 'x_size', 'y_min', 'y_size', 'z_min', 'z_size', 't_min', 't_size']), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=0), output_type=dict(), roi_file=dict(argstr='%s', extensions=None, genfile=True, hash_files=False, position=1), t_min=dict(argstr='%d', position=8), t_size=dict(argstr='%d', position=9), x_min=dict(argstr='%d', position=2), x_size=dict(argstr='%d', position=3), y_min=dict(argstr='%d', position=4), y_size=dict(argstr='%d', position=5), z_min=dict(argstr='%d', position=6), z_size=dict(argstr='%d', position=7))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), crop_list=dict(argstr='%s', position=2, xor=['x_min', 'x_size', 'y_min', 'y_size', 'z_min', 'z_size', 't_min', 't_size']), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=0), output_type=dict(), roi_file=dict(argstr='%s', extensions=None, genfile=True, hash_files=False, position=1), t_min=dict(argstr='%d', position=8), t_size=dict(argstr='%d', position=9), x_min=dict(argstr='%d', position=2), x_size=dict(argstr='%d', position=3), y_min=dict(argstr='%d', position=4), y_size=dict(argstr='%d', position=5), z_min=dict(argstr='%d', position=6), z_size=dict(argstr='%d', position=7))
```

## Next Steps


---

*Source: test_auto_ExtractROI.py:6 | Complexity: Beginner | Last updated: 2026-05-18*