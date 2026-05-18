# How To: Copygeom Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test CopyGeom inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), dest_file=dict(argstr='%s', copyfile=True, extensions=None, mandatory=True, name_source='dest_file', name_template='%s', output_name='out_file', position=1), environ=dict(nohash=True, usedefault=True), ignore_dims=dict(argstr='-d', position='-1'), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=0), output_type=dict())
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), dest_file=dict(argstr='%s', copyfile=True, extensions=None, mandatory=True, name_source='dest_file', name_template='%s', output_name='out_file', position=1), environ=dict(nohash=True, usedefault=True), ignore_dims=dict(argstr='-d', position='-1'), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=0), output_type=dict())
```

## Next Steps


---

*Source: test_auto_CopyGeom.py:6 | Complexity: Beginner | Last updated: 2026-05-18*