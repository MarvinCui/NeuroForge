# How To: Cliplevel Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test ClipLevel inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), doall=dict(argstr='-doall', position=3, xor='grad'), environ=dict(nohash=True, usedefault=True), grad=dict(argstr='-grad %s', extensions=None, position=3, xor='doall'), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-1), mfrac=dict(argstr='-mfrac %s', position=2))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), doall=dict(argstr='-doall', position=3, xor='grad'), environ=dict(nohash=True, usedefault=True), grad=dict(argstr='-grad %s', extensions=None, position=3, xor='doall'), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-1), mfrac=dict(argstr='-mfrac %s', position=2))
```

## Next Steps


---

*Source: test_auto_ClipLevel.py:6 | Complexity: Beginner | Last updated: 2026-05-18*