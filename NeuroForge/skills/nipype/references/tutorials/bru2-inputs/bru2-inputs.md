# How To: Bru2 Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Bru2 inputs

## Prerequisites

**Required Modules:**
- `bru2nii`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(actual_size=dict(argstr='-a'), append_protocol_name=dict(argstr='-p'), args=dict(argstr='%s'), compress=dict(argstr='-z'), environ=dict(nohash=True, usedefault=True), force_conversion=dict(argstr='-f'), input_dir=dict(argstr='%s', mandatory=True, position=-1), output_filename=dict(argstr='-o %s', genfile=True))
```


## Complete Example

```python
# Workflow
input_map = dict(actual_size=dict(argstr='-a'), append_protocol_name=dict(argstr='-p'), args=dict(argstr='%s'), compress=dict(argstr='-z'), environ=dict(nohash=True, usedefault=True), force_conversion=dict(argstr='-f'), input_dir=dict(argstr='%s', mandatory=True, position=-1), output_filename=dict(argstr='-o %s', genfile=True))
```

## Next Steps


---

*Source: test_auto_Bru2.py:6 | Complexity: Beginner | Last updated: 2026-05-18*