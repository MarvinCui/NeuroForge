# How To: Nwarpadjust Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test NwarpAdjust inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_files=dict(argstr='-source %s'), num_threads=dict(nohash=True, usedefault=True), out_file=dict(argstr='-prefix %s', extensions=None, keep_extension=True, name_source='in_files', name_template='%s_NwarpAdjust', requires=['in_files']), outputtype=dict(), warps=dict(argstr='-nwarp %s', mandatory=True))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_files=dict(argstr='-source %s'), num_threads=dict(nohash=True, usedefault=True), out_file=dict(argstr='-prefix %s', extensions=None, keep_extension=True, name_source='in_files', name_template='%s_NwarpAdjust', requires=['in_files']), outputtype=dict(), warps=dict(argstr='-nwarp %s', mandatory=True))
```

## Next Steps


---

*Source: test_auto_NwarpAdjust.py:6 | Complexity: Beginner | Last updated: 2026-05-18*