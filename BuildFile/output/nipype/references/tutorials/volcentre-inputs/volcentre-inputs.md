# How To: Volcentre Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Volcentre inputs

## Prerequisites

**Required Modules:**
- `minc`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), centre=dict(argstr='-centre %s %s %s'), clobber=dict(argstr='-clobber', usedefault=True), com=dict(argstr='-com'), environ=dict(nohash=True, usedefault=True), input_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), output_file=dict(argstr='%s', extensions=None, genfile=True, hash_files=False, name_source=['input_file'], name_template='%s_volcentre.mnc', position=-1), verbose=dict(argstr='-verbose'), zero_dircos=dict(argstr='-zero_dircos'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), centre=dict(argstr='-centre %s %s %s'), clobber=dict(argstr='-clobber', usedefault=True), com=dict(argstr='-com'), environ=dict(nohash=True, usedefault=True), input_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), output_file=dict(argstr='%s', extensions=None, genfile=True, hash_files=False, name_source=['input_file'], name_template='%s_volcentre.mnc', position=-1), verbose=dict(argstr='-verbose'), zero_dircos=dict(argstr='-zero_dircos'))
```

## Next Steps


---

*Source: test_auto_Volcentre.py:6 | Complexity: Beginner | Last updated: 2026-05-18*