# How To: Copy Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Copy inputs

## Prerequisites

**Required Modules:**
- `minc`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), input_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), output_file=dict(argstr='%s', extensions=None, genfile=True, hash_files=False, name_source=['input_file'], name_template='%s_copy.mnc', position=-1), pixel_values=dict(argstr='-pixel_values', xor=('pixel_values', 'real_values')), real_values=dict(argstr='-real_values', xor=('pixel_values', 'real_values')))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), input_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), output_file=dict(argstr='%s', extensions=None, genfile=True, hash_files=False, name_source=['input_file'], name_template='%s_copy.mnc', position=-1), pixel_values=dict(argstr='-pixel_values', xor=('pixel_values', 'real_values')), real_values=dict(argstr='-real_values', xor=('pixel_values', 'real_values')))
```

## Next Steps


---

*Source: test_auto_Copy.py:6 | Complexity: Beginner | Last updated: 2026-05-18*