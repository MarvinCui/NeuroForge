# How To: Masktool Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test MaskTool inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), count=dict(argstr='-count', position=2), datum=dict(argstr='-datum %s'), dilate_inputs=dict(argstr='-dilate_inputs %s'), dilate_results=dict(argstr='-dilate_results %s'), environ=dict(nohash=True, usedefault=True), fill_dirs=dict(argstr='-fill_dirs %s', requires=['fill_holes']), fill_holes=dict(argstr='-fill_holes'), frac=dict(argstr='-frac %s'), in_file=dict(argstr='-input %s', copyfile=False, mandatory=True, position=-1), inter=dict(argstr='-inter'), num_threads=dict(nohash=True, usedefault=True), out_file=dict(argstr='-prefix %s', extensions=None, name_source='in_file', name_template='%s_mask'), outputtype=dict(), union=dict(argstr='-union'), verbose=dict(argstr='-verb %s'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), count=dict(argstr='-count', position=2), datum=dict(argstr='-datum %s'), dilate_inputs=dict(argstr='-dilate_inputs %s'), dilate_results=dict(argstr='-dilate_results %s'), environ=dict(nohash=True, usedefault=True), fill_dirs=dict(argstr='-fill_dirs %s', requires=['fill_holes']), fill_holes=dict(argstr='-fill_holes'), frac=dict(argstr='-frac %s'), in_file=dict(argstr='-input %s', copyfile=False, mandatory=True, position=-1), inter=dict(argstr='-inter'), num_threads=dict(nohash=True, usedefault=True), out_file=dict(argstr='-prefix %s', extensions=None, name_source='in_file', name_template='%s_mask'), outputtype=dict(), union=dict(argstr='-union'), verbose=dict(argstr='-verb %s'))
```

## Next Steps


---

*Source: test_auto_MaskTool.py:6 | Complexity: Beginner | Last updated: 2026-05-18*