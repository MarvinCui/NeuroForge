# How To: Register Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Register inputs

## Prerequisites

**Required Modules:**
- `registration`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), curv=dict(argstr='-curv', requires=['in_smoothwm']), environ=dict(nohash=True, usedefault=True), in_smoothwm=dict(copyfile=True, extensions=None), in_sulc=dict(copyfile=True, extensions=None, mandatory=True), in_surf=dict(argstr='%s', copyfile=True, extensions=None, mandatory=True, position=-3), out_file=dict(argstr='%s', extensions=None, genfile=True, position=-1), subjects_dir=dict(), target=dict(argstr='%s', extensions=None, mandatory=True, position=-2))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), curv=dict(argstr='-curv', requires=['in_smoothwm']), environ=dict(nohash=True, usedefault=True), in_smoothwm=dict(copyfile=True, extensions=None), in_sulc=dict(copyfile=True, extensions=None, mandatory=True), in_surf=dict(argstr='%s', copyfile=True, extensions=None, mandatory=True, position=-3), out_file=dict(argstr='%s', extensions=None, genfile=True, position=-1), subjects_dir=dict(), target=dict(argstr='%s', extensions=None, mandatory=True, position=-2))
```

## Next Steps


---

*Source: test_auto_Register.py:6 | Complexity: Beginner | Last updated: 2026-05-18*