# How To: Convertdset Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test ConvertDset inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-input %s', extensions=None, mandatory=True, position=-2), num_threads=dict(nohash=True, usedefault=True), out_file=dict(argstr='-prefix %s', extensions=None, mandatory=True, position=-1), out_type=dict(argstr='-o_%s', mandatory=True, position=0), outputtype=dict())
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-input %s', extensions=None, mandatory=True, position=-2), num_threads=dict(nohash=True, usedefault=True), out_file=dict(argstr='-prefix %s', extensions=None, mandatory=True, position=-1), out_type=dict(argstr='-o_%s', mandatory=True, position=0), outputtype=dict())
```

## Next Steps


---

*Source: test_auto_ConvertDset.py:6 | Complexity: Beginner | Last updated: 2026-05-18*