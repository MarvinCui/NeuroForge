# How To: Multiimagemaths Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test MultiImageMaths inputs

## Prerequisites

**Required Modules:**
- `maths`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=2), internal_datatype=dict(argstr='-dt %s', position=1), nan2zeros=dict(argstr='-nan', position=3), op_string=dict(argstr='%s', mandatory=True, position=4), operand_files=dict(mandatory=True), out_file=dict(argstr='%s', extensions=None, genfile=True, hash_files=False, position=-2), output_datatype=dict(argstr='-odt %s', position=-1), output_type=dict())
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=2), internal_datatype=dict(argstr='-dt %s', position=1), nan2zeros=dict(argstr='-nan', position=3), op_string=dict(argstr='%s', mandatory=True, position=4), operand_files=dict(mandatory=True), out_file=dict(argstr='%s', extensions=None, genfile=True, hash_files=False, position=-2), output_datatype=dict(argstr='-odt %s', position=-1), output_type=dict())
```

## Next Steps


---

*Source: test_auto_MultiImageMaths.py:6 | Complexity: Beginner | Last updated: 2026-05-18*