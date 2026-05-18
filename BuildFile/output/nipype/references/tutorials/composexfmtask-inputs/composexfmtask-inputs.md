# How To: Composexfmtask Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test ComposeXfmTask inputs

## Prerequisites

**Required Modules:**
- `registration`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_aff=dict(argstr='-aff %s', extensions=None, mandatory=True), in_df=dict(argstr='-df %s', extensions=None, mandatory=True), out_file=dict(argstr='-out %s', extensions=None, genfile=True))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_aff=dict(argstr='-aff %s', extensions=None, mandatory=True), in_df=dict(argstr='-df %s', extensions=None, mandatory=True), out_file=dict(argstr='-out %s', extensions=None, genfile=True))
```

## Next Steps


---

*Source: test_auto_ComposeXfmTask.py:6 | Complexity: Beginner | Last updated: 2026-05-18*