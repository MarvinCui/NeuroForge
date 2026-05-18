# How To: Actpreparefsl Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test ACTPrepareFSL inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), out_file=dict(argstr='%s', extensions=None, mandatory=True, position=-1, usedefault=True))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), out_file=dict(argstr='%s', extensions=None, mandatory=True, position=-1, usedefault=True))
```

## Next Steps


---

*Source: test_auto_ACTPrepareFSL.py:6 | Complexity: Beginner | Last updated: 2026-05-18*