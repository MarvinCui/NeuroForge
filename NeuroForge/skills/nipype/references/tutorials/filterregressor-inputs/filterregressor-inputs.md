# How To: Filterregressor Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test FilterRegressor inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), design_file=dict(argstr='-d %s', extensions=None, mandatory=True, position=3), environ=dict(nohash=True, usedefault=True), filter_all=dict(argstr="-f '%s'", mandatory=True, position=4, xor=['filter_columns']), filter_columns=dict(argstr="-f '%s'", mandatory=True, position=4, xor=['filter_all']), in_file=dict(argstr='-i %s', extensions=None, mandatory=True, position=1), mask=dict(argstr='-m %s', extensions=None), out_file=dict(argstr='-o %s', extensions=None, genfile=True, hash_files=False, position=2), out_vnscales=dict(argstr='--out_vnscales'), output_type=dict(), var_norm=dict(argstr='--vn'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), design_file=dict(argstr='-d %s', extensions=None, mandatory=True, position=3), environ=dict(nohash=True, usedefault=True), filter_all=dict(argstr="-f '%s'", mandatory=True, position=4, xor=['filter_columns']), filter_columns=dict(argstr="-f '%s'", mandatory=True, position=4, xor=['filter_all']), in_file=dict(argstr='-i %s', extensions=None, mandatory=True, position=1), mask=dict(argstr='-m %s', extensions=None), out_file=dict(argstr='-o %s', extensions=None, genfile=True, hash_files=False, position=2), out_vnscales=dict(argstr='--out_vnscales'), output_type=dict(), var_norm=dict(argstr='--vn'))
```

## Next Steps


---

*Source: test_auto_FilterRegressor.py:6 | Complexity: Beginner | Last updated: 2026-05-18*