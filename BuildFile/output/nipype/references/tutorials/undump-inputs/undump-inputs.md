# How To: Undump Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Undump inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), coordinates_specification=dict(argstr='-%s'), datatype=dict(argstr='-datum %s'), default_value=dict(argstr='-dval %f'), environ=dict(nohash=True, usedefault=True), fill_value=dict(argstr='-fval %f'), head_only=dict(argstr='-head_only'), in_file=dict(argstr='-master %s', copyfile=False, extensions=None, mandatory=True, position=-1), mask_file=dict(argstr='-mask %s', extensions=None), num_threads=dict(nohash=True, usedefault=True), orient=dict(argstr='-orient %s'), out_file=dict(argstr='-prefix %s', extensions=None, name_source='in_file'), outputtype=dict(), srad=dict(argstr='-srad %f'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), coordinates_specification=dict(argstr='-%s'), datatype=dict(argstr='-datum %s'), default_value=dict(argstr='-dval %f'), environ=dict(nohash=True, usedefault=True), fill_value=dict(argstr='-fval %f'), head_only=dict(argstr='-head_only'), in_file=dict(argstr='-master %s', copyfile=False, extensions=None, mandatory=True, position=-1), mask_file=dict(argstr='-mask %s', extensions=None), num_threads=dict(nohash=True, usedefault=True), orient=dict(argstr='-orient %s'), out_file=dict(argstr='-prefix %s', extensions=None, name_source='in_file'), outputtype=dict(), srad=dict(argstr='-srad %f'))
```

## Next Steps


---

*Source: test_auto_Undump.py:6 | Complexity: Beginner | Last updated: 2026-05-18*