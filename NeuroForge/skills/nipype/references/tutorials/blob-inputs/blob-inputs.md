# How To: Blob Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Blob inputs

## Prerequisites

**Required Modules:**
- `minc`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), determinant=dict(argstr='-determinant'), environ=dict(nohash=True, usedefault=True), input_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), magnitude=dict(argstr='-magnitude'), output_file=dict(argstr='%s', extensions=None, genfile=True, hash_files=False, name_source=['input_file'], name_template='%s_blob.mnc', position=-1), trace=dict(argstr='-trace'), translation=dict(argstr='-translation'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), determinant=dict(argstr='-determinant'), environ=dict(nohash=True, usedefault=True), input_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), magnitude=dict(argstr='-magnitude'), output_file=dict(argstr='%s', extensions=None, genfile=True, hash_files=False, name_source=['input_file'], name_template='%s_blob.mnc', position=-1), trace=dict(argstr='-trace'), translation=dict(argstr='-translation'))
```

## Next Steps


---

*Source: test_auto_Blob.py:6 | Complexity: Beginner | Last updated: 2026-05-18*