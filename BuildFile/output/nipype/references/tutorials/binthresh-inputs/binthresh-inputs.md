# How To: Binthresh Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test BinThresh inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=0), inside_value=dict(argstr='%g', mandatory=True, position=4, usedefault=True), lower_bound=dict(argstr='%g', mandatory=True, position=2, usedefault=True), out_file=dict(argstr='%s', extensions=None, keep_extension=True, name_source='in_file', name_template='%s_thrbin', position=1), outside_value=dict(argstr='%g', mandatory=True, position=5, usedefault=True), upper_bound=dict(argstr='%g', mandatory=True, position=3, usedefault=True))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=0), inside_value=dict(argstr='%g', mandatory=True, position=4, usedefault=True), lower_bound=dict(argstr='%g', mandatory=True, position=2, usedefault=True), out_file=dict(argstr='%s', extensions=None, keep_extension=True, name_source='in_file', name_template='%s_thrbin', position=1), outside_value=dict(argstr='%g', mandatory=True, position=5, usedefault=True), upper_bound=dict(argstr='%g', mandatory=True, position=3, usedefault=True))
```

## Next Steps


---

*Source: test_auto_BinThresh.py:6 | Complexity: Beginner | Last updated: 2026-05-18*