# How To: Watershedskullstrip Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test WatershedSkullStrip inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), brain_atlas=dict(argstr='-brain_atlas %s', extensions=None, position=-4), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), out_file=dict(argstr='%s', extensions=None, mandatory=True, position=-1, usedefault=True), subjects_dir=dict(), t1=dict(argstr='-T1'), transform=dict(argstr='%s', extensions=None, position=-3))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), brain_atlas=dict(argstr='-brain_atlas %s', extensions=None, position=-4), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), out_file=dict(argstr='%s', extensions=None, mandatory=True, position=-1, usedefault=True), subjects_dir=dict(), t1=dict(argstr='-T1'), transform=dict(argstr='%s', extensions=None, position=-3))
```

## Next Steps


---

*Source: test_auto_WatershedSkullStrip.py:6 | Complexity: Beginner | Last updated: 2026-05-18*