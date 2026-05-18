# How To: Checktalairachalignment Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test CheckTalairachAlignment inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-xfm %s', extensions=None, mandatory=True, position=-1, xor=['subject']), subject=dict(argstr='-subj %s', mandatory=True, position=-1, xor=['in_file']), subjects_dir=dict(), threshold=dict(argstr='-T %.3f', usedefault=True))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-xfm %s', extensions=None, mandatory=True, position=-1, xor=['subject']), subject=dict(argstr='-subj %s', mandatory=True, position=-1, xor=['in_file']), subjects_dir=dict(), threshold=dict(argstr='-T %.3f', usedefault=True))
```

## Next Steps


---

*Source: test_auto_CheckTalairachAlignment.py:6 | Complexity: Beginner | Last updated: 2026-05-18*