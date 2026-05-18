# How To: Tshift Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test TShift inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), ignore=dict(argstr='-ignore %s'), in_file=dict(argstr='%s', copyfile=False, extensions=None, mandatory=True, position=-1), interp=dict(argstr='-%s'), num_threads=dict(nohash=True, usedefault=True), out_file=dict(argstr='-prefix %s', extensions=None, name_source='in_file', name_template='%s_tshift'), outputtype=dict(), rlt=dict(argstr='-rlt'), rltplus=dict(argstr='-rlt+'), slice_encoding_direction=dict(usedefault=True), slice_timing=dict(argstr='-tpattern @%s', xor=['tpattern']), tpattern=dict(argstr='-tpattern %s', xor=['slice_timing']), tr=dict(argstr='-TR %s'), tslice=dict(argstr='-slice %s', xor=['tzero']), tzero=dict(argstr='-tzero %s', xor=['tslice']))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), ignore=dict(argstr='-ignore %s'), in_file=dict(argstr='%s', copyfile=False, extensions=None, mandatory=True, position=-1), interp=dict(argstr='-%s'), num_threads=dict(nohash=True, usedefault=True), out_file=dict(argstr='-prefix %s', extensions=None, name_source='in_file', name_template='%s_tshift'), outputtype=dict(), rlt=dict(argstr='-rlt'), rltplus=dict(argstr='-rlt+'), slice_encoding_direction=dict(usedefault=True), slice_timing=dict(argstr='-tpattern @%s', xor=['tpattern']), tpattern=dict(argstr='-tpattern %s', xor=['slice_timing']), tr=dict(argstr='-TR %s'), tslice=dict(argstr='-slice %s', xor=['tzero']), tzero=dict(argstr='-tzero %s', xor=['tslice']))
```

## Next Steps


---

*Source: test_auto_TShift.py:6 | Complexity: Beginner | Last updated: 2026-05-18*