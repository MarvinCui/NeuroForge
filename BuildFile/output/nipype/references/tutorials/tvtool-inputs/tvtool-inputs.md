# How To: Tvtool Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test TVtool inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-in %s', extensions=None, mandatory=True), in_flag=dict(argstr='-%s'), out_file=dict(argstr='-out %s', extensions=None, genfile=True))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-in %s', extensions=None, mandatory=True), in_flag=dict(argstr='-%s'), out_file=dict(argstr='-out %s', extensions=None, genfile=True))
```

## Next Steps


---

*Source: test_auto_TVtool.py:6 | Complexity: Beginner | Last updated: 2026-05-18*