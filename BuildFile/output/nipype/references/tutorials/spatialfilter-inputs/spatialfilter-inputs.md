# How To: Spatialfilter Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test SpatialFilter inputs

## Prerequisites

**Required Modules:**
- `maths`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=2), internal_datatype=dict(argstr='-dt %s', position=1), kernel_file=dict(argstr='%s', extensions=None, position=5, xor=['kernel_size']), kernel_shape=dict(argstr='-kernel %s', position=4), kernel_size=dict(argstr='%.4f', position=5, xor=['kernel_file']), nan2zeros=dict(argstr='-nan', position=3), operation=dict(argstr='-f%s', mandatory=True, position=6), out_file=dict(argstr='%s', extensions=None, genfile=True, hash_files=False, position=-2), output_datatype=dict(argstr='-odt %s', position=-1), output_type=dict())
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=2), internal_datatype=dict(argstr='-dt %s', position=1), kernel_file=dict(argstr='%s', extensions=None, position=5, xor=['kernel_size']), kernel_shape=dict(argstr='-kernel %s', position=4), kernel_size=dict(argstr='%.4f', position=5, xor=['kernel_file']), nan2zeros=dict(argstr='-nan', position=3), operation=dict(argstr='-f%s', mandatory=True, position=6), out_file=dict(argstr='%s', extensions=None, genfile=True, hash_files=False, position=-2), output_datatype=dict(argstr='-odt %s', position=-1), output_type=dict())
```

## Next Steps


---

*Source: test_auto_SpatialFilter.py:6 | Complexity: Beginner | Last updated: 2026-05-18*