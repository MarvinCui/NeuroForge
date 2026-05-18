# How To: Convert Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Convert inputs

## Prerequisites

**Required Modules:**
- `minc`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), chunk=dict(argstr='-chunk %d'), clobber=dict(argstr='-clobber', usedefault=True), compression=dict(argstr='-compress %s'), environ=dict(nohash=True, usedefault=True), input_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), output_file=dict(argstr='%s', extensions=None, genfile=True, hash_files=False, name_source=['input_file'], name_template='%s_convert_output.mnc', position=-1), template=dict(argstr='-template'), two=dict(argstr='-2'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), chunk=dict(argstr='-chunk %d'), clobber=dict(argstr='-clobber', usedefault=True), compression=dict(argstr='-compress %s'), environ=dict(nohash=True, usedefault=True), input_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), output_file=dict(argstr='%s', extensions=None, genfile=True, hash_files=False, name_source=['input_file'], name_template='%s_convert_output.mnc', position=-1), template=dict(argstr='-template'), two=dict(argstr='-2'))
```

## Next Steps


---

*Source: test_auto_Convert.py:6 | Complexity: Beginner | Last updated: 2026-05-18*