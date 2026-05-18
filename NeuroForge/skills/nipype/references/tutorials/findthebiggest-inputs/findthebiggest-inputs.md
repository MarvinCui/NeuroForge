# How To: Findthebiggest Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test FindTheBiggest inputs

## Prerequisites

**Required Modules:**
- `dti`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_files=dict(argstr='%s', mandatory=True, position=0), out_file=dict(argstr='%s', extensions=None, genfile=True, hash_files=False, position=2), output_type=dict())
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_files=dict(argstr='%s', mandatory=True, position=0), out_file=dict(argstr='%s', extensions=None, genfile=True, hash_files=False, position=2), output_type=dict())
```

## Next Steps


---

*Source: test_auto_FindTheBiggest.py:6 | Complexity: Beginner | Last updated: 2026-05-18*