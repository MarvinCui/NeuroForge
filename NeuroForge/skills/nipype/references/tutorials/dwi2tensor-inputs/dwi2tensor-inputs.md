# How To: Dwi2Tensor Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test DWI2Tensor inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), debug=dict(argstr='-debug', position=1), encoding_file=dict(argstr='-grad %s', extensions=None, position=2), environ=dict(nohash=True, usedefault=True), ignore_slice_by_volume=dict(argstr='-ignoreslices %s', position=2, sep=' '), ignore_volumes=dict(argstr='-ignorevolumes %s', position=2, sep=' '), in_file=dict(argstr='%s', mandatory=True, position=-2), mask=dict(argstr='-mask %s', extensions=None), out_filename=dict(argstr='%s', extensions=None, name_source='in_file', name_template='%s_tensor.mif', output_name='tensor', position=-1), quiet=dict(argstr='-quiet', position=1))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), debug=dict(argstr='-debug', position=1), encoding_file=dict(argstr='-grad %s', extensions=None, position=2), environ=dict(nohash=True, usedefault=True), ignore_slice_by_volume=dict(argstr='-ignoreslices %s', position=2, sep=' '), ignore_volumes=dict(argstr='-ignorevolumes %s', position=2, sep=' '), in_file=dict(argstr='%s', mandatory=True, position=-2), mask=dict(argstr='-mask %s', extensions=None), out_filename=dict(argstr='%s', extensions=None, name_source='in_file', name_template='%s_tensor.mif', output_name='tensor', position=-1), quiet=dict(argstr='-quiet', position=1))
```

## Next Steps


---

*Source: test_auto_DWI2Tensor.py:6 | Complexity: Beginner | Last updated: 2026-05-18*