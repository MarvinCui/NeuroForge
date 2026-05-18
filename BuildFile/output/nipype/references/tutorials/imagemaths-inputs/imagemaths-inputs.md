# How To: Imagemaths Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test ImageMaths inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=1), in_file2=dict(argstr='%s', extensions=None, position=3), mask_file=dict(argstr='-mas %s', extensions=None), op_string=dict(argstr='%s', position=2), out_data_type=dict(argstr='-odt %s', position=-1), out_file=dict(argstr='%s', extensions=None, genfile=True, hash_files=False, position=-2), output_type=dict(), suffix=dict())
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=1), in_file2=dict(argstr='%s', extensions=None, position=3), mask_file=dict(argstr='-mas %s', extensions=None), op_string=dict(argstr='%s', position=2), out_data_type=dict(argstr='-odt %s', position=-1), out_file=dict(argstr='%s', extensions=None, genfile=True, hash_files=False, position=-2), output_type=dict(), suffix=dict())
```

## Next Steps


---

*Source: test_auto_ImageMaths.py:6 | Complexity: Beginner | Last updated: 2026-05-18*