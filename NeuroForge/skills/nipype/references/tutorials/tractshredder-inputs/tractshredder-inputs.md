# How To: Tractshredder Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test TractShredder inputs

## Prerequisites

**Required Modules:**
- `convert`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), bunchsize=dict(argstr='%d', position=2, units='NA'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='< %s', extensions=None, mandatory=True, position=-2), offset=dict(argstr='%d', position=1, units='NA'), out_file=dict(argstr='> %s', extensions=None, genfile=True, position=-1), space=dict(argstr='%d', position=3, units='NA'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), bunchsize=dict(argstr='%d', position=2, units='NA'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='< %s', extensions=None, mandatory=True, position=-2), offset=dict(argstr='%d', position=1, units='NA'), out_file=dict(argstr='> %s', extensions=None, genfile=True, position=-1), space=dict(argstr='%d', position=3, units='NA'))
```

## Next Steps


---

*Source: test_auto_TractShredder.py:6 | Complexity: Beginner | Last updated: 2026-05-18*