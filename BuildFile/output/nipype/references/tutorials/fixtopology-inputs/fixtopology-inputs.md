# How To: Fixtopology Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test FixTopology inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), copy_inputs=dict(mandatory=True), environ=dict(nohash=True, usedefault=True), ga=dict(argstr='-ga'), hemisphere=dict(argstr='%s', mandatory=True, position=-1), in_brain=dict(extensions=None, mandatory=True), in_inflated=dict(extensions=None, mandatory=True), in_orig=dict(extensions=None, mandatory=True), in_wm=dict(extensions=None, mandatory=True), mgz=dict(argstr='-mgz'), seed=dict(argstr='-seed %d'), sphere=dict(argstr='-sphere %s', extensions=None), subject_id=dict(argstr='%s', mandatory=True, position=-2, usedefault=True), subjects_dir=dict())
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), copy_inputs=dict(mandatory=True), environ=dict(nohash=True, usedefault=True), ga=dict(argstr='-ga'), hemisphere=dict(argstr='%s', mandatory=True, position=-1), in_brain=dict(extensions=None, mandatory=True), in_inflated=dict(extensions=None, mandatory=True), in_orig=dict(extensions=None, mandatory=True), in_wm=dict(extensions=None, mandatory=True), mgz=dict(argstr='-mgz'), seed=dict(argstr='-seed %d'), sphere=dict(argstr='-sphere %s', extensions=None), subject_id=dict(argstr='%s', mandatory=True, position=-2, usedefault=True), subjects_dir=dict())
```

## Next Steps


---

*Source: test_auto_FixTopology.py:6 | Complexity: Beginner | Last updated: 2026-05-18*