# How To: Replacefswithfirst Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test ReplaceFSwithFIRST inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_config=dict(argstr='%s', extensions=None, position=-2), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-4), in_t1w=dict(argstr='%s', extensions=None, mandatory=True, position=-3), out_file=dict(argstr='%s', extensions=None, mandatory=True, position=-1, usedefault=True))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_config=dict(argstr='%s', extensions=None, position=-2), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-4), in_t1w=dict(argstr='%s', extensions=None, mandatory=True, position=-3), out_file=dict(argstr='%s', extensions=None, mandatory=True, position=-1, usedefault=True))
```

## Next Steps


---

*Source: test_auto_ReplaceFSwithFIRST.py:6 | Complexity: Beginner | Last updated: 2026-05-18*