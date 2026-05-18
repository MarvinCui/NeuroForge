# How To: Lfcd Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test LFCD inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), autoclip=dict(argstr='-autoclip'), automask=dict(argstr='-automask'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', copyfile=False, extensions=None, mandatory=True, position=-1), mask=dict(argstr='-mask %s', extensions=None), num_threads=dict(nohash=True, usedefault=True), out_file=dict(argstr='-prefix %s', extensions=None, name_source=['in_file'], name_template='%s_afni'), outputtype=dict(), polort=dict(argstr='-polort %d'), thresh=dict(argstr='-thresh %f'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), autoclip=dict(argstr='-autoclip'), automask=dict(argstr='-automask'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', copyfile=False, extensions=None, mandatory=True, position=-1), mask=dict(argstr='-mask %s', extensions=None), num_threads=dict(nohash=True, usedefault=True), out_file=dict(argstr='-prefix %s', extensions=None, name_source=['in_file'], name_template='%s_afni'), outputtype=dict(), polort=dict(argstr='-polort %d'), thresh=dict(argstr='-thresh %f'))
```

## Next Steps


---

*Source: test_auto_LFCD.py:6 | Complexity: Beginner | Last updated: 2026-05-18*