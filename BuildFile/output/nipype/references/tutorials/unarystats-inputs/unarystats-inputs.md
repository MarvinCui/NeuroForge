# How To: Unarystats Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test UnaryStats inputs

## Prerequisites

**Required Modules:**
- `stats`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=2), larger_voxel=dict(argstr='-t %f', position=-3), mask_file=dict(argstr='-m %s', extensions=None, position=-2), operation=dict(argstr='-%s', mandatory=True, position=4))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=2), larger_voxel=dict(argstr='-t %f', position=-3), mask_file=dict(argstr='-m %s', extensions=None, position=-2), operation=dict(argstr='-%s', mandatory=True, position=4))
```

## Next Steps


---

*Source: test_auto_UnaryStats.py:6 | Complexity: Beginner | Last updated: 2026-05-18*