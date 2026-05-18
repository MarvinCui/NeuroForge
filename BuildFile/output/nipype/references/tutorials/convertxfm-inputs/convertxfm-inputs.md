# How To: Convertxfm Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test ConvertXFM inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), concat_xfm=dict(argstr='-concat', position=-3, requires=['in_file2'], xor=['invert_xfm', 'concat_xfm', 'fix_scale_skew']), environ=dict(nohash=True, usedefault=True), fix_scale_skew=dict(argstr='-fixscaleskew', position=-3, requires=['in_file2'], xor=['invert_xfm', 'concat_xfm', 'fix_scale_skew']), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-1), in_file2=dict(argstr='%s', extensions=None, position=-2), invert_xfm=dict(argstr='-inverse', position=-3, xor=['invert_xfm', 'concat_xfm', 'fix_scale_skew']), out_file=dict(argstr='-omat %s', extensions=None, genfile=True, hash_files=False, position=1), output_type=dict())
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), concat_xfm=dict(argstr='-concat', position=-3, requires=['in_file2'], xor=['invert_xfm', 'concat_xfm', 'fix_scale_skew']), environ=dict(nohash=True, usedefault=True), fix_scale_skew=dict(argstr='-fixscaleskew', position=-3, requires=['in_file2'], xor=['invert_xfm', 'concat_xfm', 'fix_scale_skew']), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-1), in_file2=dict(argstr='%s', extensions=None, position=-2), invert_xfm=dict(argstr='-inverse', position=-3, xor=['invert_xfm', 'concat_xfm', 'fix_scale_skew']), out_file=dict(argstr='-omat %s', extensions=None, genfile=True, hash_files=False, position=1), output_type=dict())
```

## Next Steps


---

*Source: test_auto_ConvertXFM.py:6 | Complexity: Beginner | Last updated: 2026-05-18*