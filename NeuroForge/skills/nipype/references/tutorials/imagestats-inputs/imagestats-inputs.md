# How To: Imagestats Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test ImageStats inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=3), index_mask_file=dict(argstr='-K %s', extensions=None, position=2), mask_file=dict(argstr='', extensions=None), op_string=dict(argstr='%s', mandatory=True, position=4), output_type=dict(), split_4d=dict(argstr='-t', position=1))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=3), index_mask_file=dict(argstr='-K %s', extensions=None, position=2), mask_file=dict(argstr='', extensions=None), op_string=dict(argstr='%s', mandatory=True, position=4), output_type=dict(), split_4d=dict(argstr='-t', position=1))
```

## Next Steps


---

*Source: test_auto_ImageStats.py:6 | Complexity: Beginner | Last updated: 2026-05-18*