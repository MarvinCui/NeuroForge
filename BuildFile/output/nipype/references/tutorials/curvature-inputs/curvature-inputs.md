# How To: Curvature Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Curvature inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), averages=dict(argstr='-a %d'), copy_input=dict(), distances=dict(argstr='-distances %d %d'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', copyfile=True, extensions=None, mandatory=True, position=-2), n=dict(argstr='-n'), save=dict(argstr='-w'), subjects_dir=dict(), threshold=dict(argstr='-thresh %.3f'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), averages=dict(argstr='-a %d'), copy_input=dict(), distances=dict(argstr='-distances %d %d'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', copyfile=True, extensions=None, mandatory=True, position=-2), n=dict(argstr='-n'), save=dict(argstr='-w'), subjects_dir=dict(), threshold=dict(argstr='-thresh %.3f'))
```

## Next Steps


---

*Source: test_auto_Curvature.py:6 | Complexity: Beginner | Last updated: 2026-05-18*