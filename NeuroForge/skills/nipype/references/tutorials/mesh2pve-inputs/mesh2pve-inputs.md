# How To: Mesh2Pve Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Mesh2PVE inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-3), in_first=dict(argstr='-first %s', extensions=None), out_file=dict(argstr='%s', extensions=None, mandatory=True, position=-1, usedefault=True), reference=dict(argstr='%s', extensions=None, mandatory=True, position=-2))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-3), in_first=dict(argstr='-first %s', extensions=None), out_file=dict(argstr='%s', extensions=None, mandatory=True, position=-1, usedefault=True), reference=dict(argstr='%s', extensions=None, mandatory=True, position=-2))
```

## Next Steps


---

*Source: test_auto_Mesh2PVE.py:6 | Complexity: Beginner | Last updated: 2026-05-18*