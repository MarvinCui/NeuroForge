# How To: Addxformtoheader Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test AddXFormToHeader inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), copy_name=dict(argstr='-c'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), out_file=dict(argstr='%s', extensions=None, position=-1, usedefault=True), subjects_dir=dict(), transform=dict(argstr='%s', extensions=None, mandatory=True, position=-3), verbose=dict(argstr='-v'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), copy_name=dict(argstr='-c'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), out_file=dict(argstr='%s', extensions=None, position=-1, usedefault=True), subjects_dir=dict(), transform=dict(argstr='%s', extensions=None, mandatory=True, position=-3), verbose=dict(argstr='-v'))
```

## Next Steps


---

*Source: test_auto_AddXFormToHeader.py:6 | Complexity: Beginner | Last updated: 2026-05-18*