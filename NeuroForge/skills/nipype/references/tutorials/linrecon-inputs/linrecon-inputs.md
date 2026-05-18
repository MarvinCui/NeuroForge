# How To: Linrecon Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test LinRecon inputs

## Prerequisites

**Required Modules:**
- `odf`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), bgmask=dict(argstr='-bgmask %s', extensions=None), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=1), log=dict(argstr='-log'), normalize=dict(argstr='-normalize'), out_file=dict(argstr='> %s', extensions=None, genfile=True, position=-1), qball_mat=dict(argstr='%s', extensions=None, mandatory=True, position=3), scheme_file=dict(argstr='%s', extensions=None, mandatory=True, position=2))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), bgmask=dict(argstr='-bgmask %s', extensions=None), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=1), log=dict(argstr='-log'), normalize=dict(argstr='-normalize'), out_file=dict(argstr='> %s', extensions=None, genfile=True, position=-1), qball_mat=dict(argstr='%s', extensions=None, mandatory=True, position=3), scheme_file=dict(argstr='%s', extensions=None, mandatory=True, position=2))
```

## Next Steps


---

*Source: test_auto_LinRecon.py:6 | Complexity: Beginner | Last updated: 2026-05-18*