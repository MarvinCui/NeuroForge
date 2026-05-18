# How To: Fitmsparams Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test FitMSParams inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), flip_list=dict(), in_files=dict(argstr='%s', mandatory=True, position=-2), out_dir=dict(argstr='%s', genfile=True, position=-1), subjects_dir=dict(), te_list=dict(), tr_list=dict(), xfm_list=dict())
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), flip_list=dict(), in_files=dict(argstr='%s', mandatory=True, position=-2), out_dir=dict(argstr='%s', genfile=True, position=-1), subjects_dir=dict(), te_list=dict(), tr_list=dict(), xfm_list=dict())
```

## Next Steps


---

*Source: test_auto_FitMSParams.py:6 | Complexity: Beginner | Last updated: 2026-05-18*