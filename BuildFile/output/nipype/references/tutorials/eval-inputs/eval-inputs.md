# How To: Eval Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Eval inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), expr=dict(argstr='-expr "%s"', mandatory=True, position=3), in_file_a=dict(argstr='-a %s', extensions=None, mandatory=True, position=0), in_file_b=dict(argstr='-b %s', extensions=None, position=1), in_file_c=dict(argstr='-c %s', extensions=None, position=2), num_threads=dict(nohash=True, usedefault=True), other=dict(argstr='', extensions=None), out1D=dict(argstr='-1D'), out_file=dict(argstr='-prefix %s', extensions=None, name_source='in_file_a', name_template='%s_calc'), outputtype=dict(), single_idx=dict(), start_idx=dict(requires=['stop_idx']), stop_idx=dict(requires=['start_idx']))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), expr=dict(argstr='-expr "%s"', mandatory=True, position=3), in_file_a=dict(argstr='-a %s', extensions=None, mandatory=True, position=0), in_file_b=dict(argstr='-b %s', extensions=None, position=1), in_file_c=dict(argstr='-c %s', extensions=None, position=2), num_threads=dict(nohash=True, usedefault=True), other=dict(argstr='', extensions=None), out1D=dict(argstr='-1D'), out_file=dict(argstr='-prefix %s', extensions=None, name_source='in_file_a', name_template='%s_calc'), outputtype=dict(), single_idx=dict(), start_idx=dict(requires=['stop_idx']), stop_idx=dict(requires=['start_idx']))
```

## Next Steps


---

*Source: test_auto_Eval.py:6 | Complexity: Beginner | Last updated: 2026-05-18*