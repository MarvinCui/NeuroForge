# How To: Training Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Training inputs

## Prerequisites

**Required Modules:**
- `fix`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), loo=dict(argstr='-l', position=2), mel_icas=dict(argstr='%s', copyfile=False, position=-1), trained_wts_filestem=dict(argstr='%s', position=1))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), loo=dict(argstr='-l', position=2), mel_icas=dict(argstr='%s', copyfile=False, position=-1), trained_wts_filestem=dict(argstr='%s', position=1))
```

## Next Steps


---

*Source: test_auto_Training.py:6 | Complexity: Beginner | Last updated: 2026-05-18*