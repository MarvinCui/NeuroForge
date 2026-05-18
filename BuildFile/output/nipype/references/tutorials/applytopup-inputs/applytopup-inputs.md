# How To: Applytopup Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test ApplyTOPUP inputs

## Prerequisites

**Required Modules:**
- `epi`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), datatype=dict(argstr='-d=%s'), encoding_file=dict(argstr='--datain=%s', extensions=None, mandatory=True), environ=dict(nohash=True, usedefault=True), in_files=dict(argstr='--imain=%s', mandatory=True, sep=','), in_index=dict(argstr='--inindex=%s', sep=','), in_topup_fieldcoef=dict(argstr='--topup=%s', copyfile=False, extensions=None, requires=['in_topup_movpar']), in_topup_movpar=dict(copyfile=False, extensions=None, requires=['in_topup_fieldcoef']), interp=dict(argstr='--interp=%s'), method=dict(argstr='--method=%s'), out_corrected=dict(argstr='--out=%s', extensions=None, name_source=['in_files'], name_template='%s_corrected'), output_type=dict())
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), datatype=dict(argstr='-d=%s'), encoding_file=dict(argstr='--datain=%s', extensions=None, mandatory=True), environ=dict(nohash=True, usedefault=True), in_files=dict(argstr='--imain=%s', mandatory=True, sep=','), in_index=dict(argstr='--inindex=%s', sep=','), in_topup_fieldcoef=dict(argstr='--topup=%s', copyfile=False, extensions=None, requires=['in_topup_movpar']), in_topup_movpar=dict(copyfile=False, extensions=None, requires=['in_topup_fieldcoef']), interp=dict(argstr='--interp=%s'), method=dict(argstr='--method=%s'), out_corrected=dict(argstr='--out=%s', extensions=None, name_source=['in_files'], name_template='%s_corrected'), output_type=dict())
```

## Next Steps


---

*Source: test_auto_ApplyTOPUP.py:6 | Complexity: Beginner | Last updated: 2026-05-18*