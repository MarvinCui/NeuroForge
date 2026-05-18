# How To: C3Daffinetool Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test C3dAffineTool inputs

## Prerequisites

**Required Modules:**
- `c3`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), fsl2ras=dict(argstr='-fsl2ras', position=4), itk_transform=dict(argstr='-oitk %s', hash_files=False, position=5), reference_file=dict(argstr='-ref %s', extensions=None, position=1), source_file=dict(argstr='-src %s', extensions=None, position=2), transform_file=dict(argstr='%s', extensions=None, position=3))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), fsl2ras=dict(argstr='-fsl2ras', position=4), itk_transform=dict(argstr='-oitk %s', hash_files=False, position=5), reference_file=dict(argstr='-ref %s', extensions=None, position=1), source_file=dict(argstr='-src %s', extensions=None, position=2), transform_file=dict(argstr='%s', extensions=None, position=3))
```

## Next Steps


---

*Source: test_auto_C3dAffineTool.py:6 | Complexity: Beginner | Last updated: 2026-05-18*