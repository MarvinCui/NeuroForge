# How To: Mrconvert Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test MRConvert inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), extension=dict(position=2, usedefault=True), extract_at_axis=dict(argstr='-coord %s', position=1), extract_at_coordinate=dict(argstr='%s', position=2, sep=','), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), layout=dict(argstr='-output %s', position=2), offset_bias=dict(argstr='-scale %d', position=3, units='mm'), out_filename=dict(argstr='%s', extensions=None, genfile=True, position=-1), output_datatype=dict(argstr='-output %s', position=2), prs=dict(argstr='-prs', position=3), replace_NaN_with_zero=dict(argstr='-zero', position=3), resample=dict(argstr='-scale %d', position=3, units='mm'), voxel_dims=dict(argstr='-vox %s', position=3, sep=','))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), extension=dict(position=2, usedefault=True), extract_at_axis=dict(argstr='-coord %s', position=1), extract_at_coordinate=dict(argstr='%s', position=2, sep=','), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), layout=dict(argstr='-output %s', position=2), offset_bias=dict(argstr='-scale %d', position=3, units='mm'), out_filename=dict(argstr='%s', extensions=None, genfile=True, position=-1), output_datatype=dict(argstr='-output %s', position=2), prs=dict(argstr='-prs', position=3), replace_NaN_with_zero=dict(argstr='-zero', position=3), resample=dict(argstr='-scale %d', position=3, units='mm'), voxel_dims=dict(argstr='-vox %s', position=3, sep=','))
```

## Next Steps


---

*Source: test_auto_MRConvert.py:6 | Complexity: Beginner | Last updated: 2026-05-18*