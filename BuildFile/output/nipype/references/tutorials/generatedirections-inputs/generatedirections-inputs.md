# How To: Generatedirections Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test GenerateDirections inputs

## Prerequisites

**Required Modules:**
- `tensors`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), display_debug=dict(argstr='-debug'), display_info=dict(argstr='-info'), environ=dict(nohash=True, usedefault=True), niter=dict(argstr='-niter %s'), num_dirs=dict(argstr='%s', mandatory=True, position=-2), out_file=dict(argstr='%s', extensions=None, hash_files=False, name_source=['num_dirs'], name_template='directions_%d.txt', position=-1), power=dict(argstr='-power %s'), quiet_display=dict(argstr='-quiet'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), display_debug=dict(argstr='-debug'), display_info=dict(argstr='-info'), environ=dict(nohash=True, usedefault=True), niter=dict(argstr='-niter %s'), num_dirs=dict(argstr='%s', mandatory=True, position=-2), out_file=dict(argstr='%s', extensions=None, hash_files=False, name_source=['num_dirs'], name_template='directions_%d.txt', position=-1), power=dict(argstr='-power %s'), quiet_display=dict(argstr='-quiet'))
```

## Next Steps


---

*Source: test_auto_GenerateDirections.py:6 | Complexity: Beginner | Last updated: 2026-05-18*