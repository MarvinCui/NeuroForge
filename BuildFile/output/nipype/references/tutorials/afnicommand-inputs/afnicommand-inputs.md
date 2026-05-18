# How To: Afnicommand Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test AFNICommand inputs

## Prerequisites

**Required Modules:**
- `base`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), num_threads=dict(nohash=True, usedefault=True), out_file=dict(argstr='-prefix %s', extensions=None, name_source=['in_file'], name_template='%s_afni'), outputtype=dict())
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), num_threads=dict(nohash=True, usedefault=True), out_file=dict(argstr='-prefix %s', extensions=None, name_source=['in_file'], name_template='%s_afni'), outputtype=dict())
```

## Next Steps


---

*Source: test_auto_AFNICommand.py:6 | Complexity: Beginner | Last updated: 2026-05-18*