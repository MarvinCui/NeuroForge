# How To: Smooth Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Smooth inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), fwhm=dict(argstr='-kernel gauss %.03f -fmean', mandatory=True, position=1, xor=['sigma']), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=0), output_type=dict(), sigma=dict(argstr='-kernel gauss %.03f -fmean', mandatory=True, position=1, xor=['fwhm']), smoothed_file=dict(argstr='%s', extensions=None, hash_files=False, name_source=['in_file'], name_template='%s_smooth', position=2))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), fwhm=dict(argstr='-kernel gauss %.03f -fmean', mandatory=True, position=1, xor=['sigma']), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=0), output_type=dict(), sigma=dict(argstr='-kernel gauss %.03f -fmean', mandatory=True, position=1, xor=['fwhm']), smoothed_file=dict(argstr='%s', extensions=None, hash_files=False, name_source=['in_file'], name_template='%s_smooth', position=2))
```

## Next Steps


---

*Source: test_auto_Smooth.py:6 | Complexity: Beginner | Last updated: 2026-05-18*