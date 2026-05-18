# How To: Preparefieldmap Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test PrepareFieldmap inputs

## Prerequisites

**Required Modules:**
- `epi`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), delta_TE=dict(argstr='%f', mandatory=True, position=-2, usedefault=True), environ=dict(nohash=True, usedefault=True), in_magnitude=dict(argstr='%s', extensions=None, mandatory=True, position=3), in_phase=dict(argstr='%s', extensions=None, mandatory=True, position=2), nocheck=dict(argstr='--nocheck', position=-1, usedefault=True), out_fieldmap=dict(argstr='%s', extensions=None, position=4), output_type=dict(), scanner=dict(argstr='%s', position=1, usedefault=True))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), delta_TE=dict(argstr='%f', mandatory=True, position=-2, usedefault=True), environ=dict(nohash=True, usedefault=True), in_magnitude=dict(argstr='%s', extensions=None, mandatory=True, position=3), in_phase=dict(argstr='%s', extensions=None, mandatory=True, position=2), nocheck=dict(argstr='--nocheck', position=-1, usedefault=True), out_fieldmap=dict(argstr='%s', extensions=None, position=4), output_type=dict(), scanner=dict(argstr='%s', position=1, usedefault=True))
```

## Next Steps


---

*Source: test_auto_PrepareFieldmap.py:6 | Complexity: Beginner | Last updated: 2026-05-18*