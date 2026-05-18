# How To: Mriscombine Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test MRIsCombine inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_files=dict(argstr='--combinesurfs %s', mandatory=True, position=1), out_file=dict(argstr='%s', extensions=None, genfile=True, mandatory=True, position=-1), subjects_dir=dict())
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_files=dict(argstr='--combinesurfs %s', mandatory=True, position=1), out_file=dict(argstr='%s', extensions=None, genfile=True, mandatory=True, position=-1), subjects_dir=dict())
```

## Next Steps


---

*Source: test_auto_MRIsCombine.py:6 | Complexity: Beginner | Last updated: 2026-05-18*