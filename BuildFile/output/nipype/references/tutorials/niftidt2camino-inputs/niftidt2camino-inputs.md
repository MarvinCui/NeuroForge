# How To: Niftidt2Camino Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test NIfTIDT2Camino inputs

## Prerequisites

**Required Modules:**
- `convert`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), bgmask=dict(argstr='-bgmask %s', extensions=None), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-inputfile %s', extensions=None, mandatory=True, position=1), lns0_file=dict(argstr='-lns0 %s', extensions=None), out_file=dict(argstr='> %s', extensions=None, genfile=True, position=-1), s0_file=dict(argstr='-s0 %s', extensions=None), scaleinter=dict(argstr='-scaleinter %s'), scaleslope=dict(argstr='-scaleslope %s'), uppertriangular=dict(argstr='-uppertriangular %s'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), bgmask=dict(argstr='-bgmask %s', extensions=None), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-inputfile %s', extensions=None, mandatory=True, position=1), lns0_file=dict(argstr='-lns0 %s', extensions=None), out_file=dict(argstr='> %s', extensions=None, genfile=True, position=-1), s0_file=dict(argstr='-s0 %s', extensions=None), scaleinter=dict(argstr='-scaleinter %s'), scaleslope=dict(argstr='-scaleslope %s'), uppertriangular=dict(argstr='-uppertriangular %s'))
```

## Next Steps


---

*Source: test_auto_NIfTIDT2Camino.py:6 | Complexity: Beginner | Last updated: 2026-05-18*