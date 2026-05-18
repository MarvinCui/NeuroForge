# How To: Generatewhitemattermask Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test GenerateWhiteMatterMask inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), binary_mask=dict(argstr='%s', extensions=None, mandatory=True, position=-2), encoding_file=dict(argstr='-grad %s', extensions=None, mandatory=True, position=1), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-3), noise_level_margin=dict(argstr='-margin %s'), out_WMProb_filename=dict(argstr='%s', extensions=None, genfile=True, position=-1))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), binary_mask=dict(argstr='%s', extensions=None, mandatory=True, position=-2), encoding_file=dict(argstr='-grad %s', extensions=None, mandatory=True, position=1), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-3), noise_level_margin=dict(argstr='-margin %s'), out_WMProb_filename=dict(argstr='%s', extensions=None, genfile=True, position=-1))
```

## Next Steps


---

*Source: test_auto_GenerateWhiteMatterMask.py:6 | Complexity: Beginner | Last updated: 2026-05-18*