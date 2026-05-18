# How To: Volpad Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Volpad inputs

## Prerequisites

**Required Modules:**
- `minc`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), auto=dict(argstr='-auto'), auto_freq=dict(argstr='-auto_freq %s'), clobber=dict(argstr='-clobber', usedefault=True), distance=dict(argstr='-distance %s'), environ=dict(nohash=True, usedefault=True), input_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), output_file=dict(argstr='%s', extensions=None, genfile=True, hash_files=False, name_source=['input_file'], name_template='%s_volpad.mnc', position=-1), smooth=dict(argstr='-smooth'), smooth_distance=dict(argstr='-smooth_distance %s'), verbose=dict(argstr='-verbose'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), auto=dict(argstr='-auto'), auto_freq=dict(argstr='-auto_freq %s'), clobber=dict(argstr='-clobber', usedefault=True), distance=dict(argstr='-distance %s'), environ=dict(nohash=True, usedefault=True), input_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), output_file=dict(argstr='%s', extensions=None, genfile=True, hash_files=False, name_source=['input_file'], name_template='%s_volpad.mnc', position=-1), smooth=dict(argstr='-smooth'), smooth_distance=dict(argstr='-smooth_distance %s'), verbose=dict(argstr='-verbose'))
```

## Next Steps


---

*Source: test_auto_Volpad.py:6 | Complexity: Beginner | Last updated: 2026-05-18*