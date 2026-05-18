# How To: Dt2Nifti Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test DT2NIfTI inputs

## Prerequisites

**Required Modules:**
- `convert`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), header_file=dict(argstr='-header %s', extensions=None, mandatory=True, position=3), in_file=dict(argstr='-inputfile %s', extensions=None, mandatory=True, position=1), output_root=dict(argstr='-outputroot %s', extensions=None, genfile=True, position=2))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), header_file=dict(argstr='-header %s', extensions=None, mandatory=True, position=3), in_file=dict(argstr='-inputfile %s', extensions=None, mandatory=True, position=1), output_root=dict(argstr='-outputroot %s', extensions=None, genfile=True, position=2))
```

## Next Steps


---

*Source: test_auto_DT2NIfTI.py:6 | Complexity: Beginner | Last updated: 2026-05-18*