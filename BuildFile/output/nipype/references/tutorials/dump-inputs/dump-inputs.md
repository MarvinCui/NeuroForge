# How To: Dump Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Dump inputs

## Prerequisites

**Required Modules:**
- `minc`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(annotations_brief=dict(argstr='-b %s', xor=('annotations_brief', 'annotations_full')), annotations_full=dict(argstr='-f %s', xor=('annotations_brief', 'annotations_full')), args=dict(argstr='%s'), coordinate_data=dict(argstr='-c', xor=('coordinate_data', 'header_data')), environ=dict(nohash=True, usedefault=True), header_data=dict(argstr='-h', xor=('coordinate_data', 'header_data')), input_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), line_length=dict(argstr='-l %d'), netcdf_name=dict(argstr='-n %s'), out_file=dict(argstr='> %s', extensions=None, genfile=True, position=-1), output_file=dict(extensions=None, hash_files=False, keep_extension=False, name_source=['input_file'], name_template='%s_dump.txt', position=-1), precision=dict(argstr='%s'), variables=dict(argstr='-v %s', sep=','))
```


## Complete Example

```python
# Workflow
input_map = dict(annotations_brief=dict(argstr='-b %s', xor=('annotations_brief', 'annotations_full')), annotations_full=dict(argstr='-f %s', xor=('annotations_brief', 'annotations_full')), args=dict(argstr='%s'), coordinate_data=dict(argstr='-c', xor=('coordinate_data', 'header_data')), environ=dict(nohash=True, usedefault=True), header_data=dict(argstr='-h', xor=('coordinate_data', 'header_data')), input_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), line_length=dict(argstr='-l %d'), netcdf_name=dict(argstr='-n %s'), out_file=dict(argstr='> %s', extensions=None, genfile=True, position=-1), output_file=dict(extensions=None, hash_files=False, keep_extension=False, name_source=['input_file'], name_template='%s_dump.txt', position=-1), precision=dict(argstr='%s'), variables=dict(argstr='-v %s', sep=','))
```

## Next Steps


---

*Source: test_auto_Dump.py:6 | Complexity: Beginner | Last updated: 2026-05-18*