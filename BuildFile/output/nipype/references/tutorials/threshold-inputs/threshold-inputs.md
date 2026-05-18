# How To: Threshold Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Threshold inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(absolute_threshold_value=dict(argstr='-abs %s'), args=dict(argstr='%s'), debug=dict(argstr='-debug', position=1), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), invert=dict(argstr='-invert', position=1), out_filename=dict(argstr='%s', extensions=None, genfile=True, position=-1), percentage_threshold_value=dict(argstr='-percent %s'), quiet=dict(argstr='-quiet', position=1), replace_zeros_with_NaN=dict(argstr='-nan', position=1))
```


## Complete Example

```python
# Workflow
input_map = dict(absolute_threshold_value=dict(argstr='-abs %s'), args=dict(argstr='%s'), debug=dict(argstr='-debug', position=1), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), invert=dict(argstr='-invert', position=1), out_filename=dict(argstr='%s', extensions=None, genfile=True, position=-1), percentage_threshold_value=dict(argstr='-percent %s'), quiet=dict(argstr='-quiet', position=1), replace_zeros_with_NaN=dict(argstr='-nan', position=1))
```

## Next Steps


---

*Source: test_auto_Threshold.py:6 | Complexity: Beginner | Last updated: 2026-05-18*