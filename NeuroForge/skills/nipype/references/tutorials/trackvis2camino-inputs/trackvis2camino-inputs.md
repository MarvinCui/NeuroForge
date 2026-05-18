# How To: Trackvis2Camino Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Trackvis2Camino inputs

## Prerequisites

**Required Modules:**
- `convert`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(append_file=dict(argstr='-a %s', extensions=None, position=2), args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-i %s', extensions=None, mandatory=True, position=1), out_file=dict(argstr='-o %s', extensions=None, genfile=True, position=2))
```


## Complete Example

```python
# Workflow
input_map = dict(append_file=dict(argstr='-a %s', extensions=None, position=2), args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-i %s', extensions=None, mandatory=True, position=1), out_file=dict(argstr='-o %s', extensions=None, genfile=True, position=2))
```

## Next Steps


---

*Source: test_auto_Trackvis2Camino.py:6 | Complexity: Beginner | Last updated: 2026-05-18*