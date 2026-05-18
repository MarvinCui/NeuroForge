# How To: Bigaverage Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test BigAverage inputs

## Prerequisites

**Required Modules:**
- `minc`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), clobber=dict(argstr='--clobber', usedefault=True), environ=dict(nohash=True, usedefault=True), input_files=dict(argstr='%s', mandatory=True, position=-2, sep=' '), output_file=dict(argstr='%s', extensions=None, genfile=True, hash_files=False, name_source=['input_files'], name_template='%s_bigaverage.mnc', position=-1), output_float=dict(argstr='--float'), robust=dict(argstr='-robust'), sd_file=dict(argstr='--sdfile %s', extensions=None, hash_files=False, name_source=['input_files'], name_template='%s_bigaverage_stdev.mnc'), tmpdir=dict(argstr='-tmpdir %s'), verbose=dict(argstr='--verbose'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), clobber=dict(argstr='--clobber', usedefault=True), environ=dict(nohash=True, usedefault=True), input_files=dict(argstr='%s', mandatory=True, position=-2, sep=' '), output_file=dict(argstr='%s', extensions=None, genfile=True, hash_files=False, name_source=['input_files'], name_template='%s_bigaverage.mnc', position=-1), output_float=dict(argstr='--float'), robust=dict(argstr='-robust'), sd_file=dict(argstr='--sdfile %s', extensions=None, hash_files=False, name_source=['input_files'], name_template='%s_bigaverage_stdev.mnc'), tmpdir=dict(argstr='-tmpdir %s'), verbose=dict(argstr='--verbose'))
```

## Next Steps


---

*Source: test_auto_BigAverage.py:6 | Complexity: Beginner | Last updated: 2026-05-18*