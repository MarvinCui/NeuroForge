# How To: Tstat Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test TStat inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', copyfile=False, extensions=None, mandatory=True, position=-1), mask=dict(argstr='-mask %s', extensions=None), num_threads=dict(nohash=True, usedefault=True), options=dict(argstr='%s'), out_file=dict(argstr='-prefix %s', extensions=None, name_source='in_file', name_template='%s_tstat'), outputtype=dict())
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', copyfile=False, extensions=None, mandatory=True, position=-1), mask=dict(argstr='-mask %s', extensions=None), num_threads=dict(nohash=True, usedefault=True), options=dict(argstr='%s'), out_file=dict(argstr='-prefix %s', extensions=None, name_source='in_file', name_template='%s_tstat'), outputtype=dict())
```

## Next Steps


---

*Source: test_auto_TStat.py:6 | Complexity: Beginner | Last updated: 2026-05-18*