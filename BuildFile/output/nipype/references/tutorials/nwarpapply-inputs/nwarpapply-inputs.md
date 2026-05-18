# How To: Nwarpapply Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test NwarpApply inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(ainterp=dict(argstr='-ainterp %s'), args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-source %s', mandatory=True), interp=dict(argstr='-interp %s', usedefault=True), inv_warp=dict(argstr='-iwarp'), master=dict(argstr='-master %s', extensions=None), out_file=dict(argstr='-prefix %s', extensions=None, name_source='in_file', name_template='%s_Nwarp'), quiet=dict(argstr='-quiet', xor=['verb']), short=dict(argstr='-short'), verb=dict(argstr='-verb', xor=['quiet']), warp=dict(argstr='-nwarp %s', mandatory=True))
```


## Complete Example

```python
# Workflow
input_map = dict(ainterp=dict(argstr='-ainterp %s'), args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-source %s', mandatory=True), interp=dict(argstr='-interp %s', usedefault=True), inv_warp=dict(argstr='-iwarp'), master=dict(argstr='-master %s', extensions=None), out_file=dict(argstr='-prefix %s', extensions=None, name_source='in_file', name_template='%s_Nwarp'), quiet=dict(argstr='-quiet', xor=['verb']), short=dict(argstr='-short'), verb=dict(argstr='-verb', xor=['quiet']), warp=dict(argstr='-nwarp %s', mandatory=True))
```

## Next Steps


---

*Source: test_auto_NwarpApply.py:6 | Complexity: Beginner | Last updated: 2026-05-18*