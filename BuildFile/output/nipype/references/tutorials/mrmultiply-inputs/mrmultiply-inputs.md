# How To: Mrmultiply Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test MRMultiply inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), debug=dict(argstr='-debug', position=1), environ=dict(nohash=True, usedefault=True), in_files=dict(argstr='%s', mandatory=True, position=-2), out_filename=dict(argstr='%s', extensions=None, genfile=True, position=-1), quiet=dict(argstr='-quiet', position=1))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), debug=dict(argstr='-debug', position=1), environ=dict(nohash=True, usedefault=True), in_files=dict(argstr='%s', mandatory=True, position=-2), out_filename=dict(argstr='%s', extensions=None, genfile=True, position=-1), quiet=dict(argstr='-quiet', position=1))
```

## Next Steps


---

*Source: test_auto_MRMultiply.py:6 | Complexity: Beginner | Last updated: 2026-05-18*