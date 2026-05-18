# How To: Tcat Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test TCat inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_files=dict(argstr=' %s', copyfile=False, mandatory=True, position=-1), num_threads=dict(nohash=True, usedefault=True), out_file=dict(argstr='-prefix %s', extensions=None, name_source='in_files', name_template='%s_tcat'), outputtype=dict(), rlt=dict(argstr='-rlt%s', position=1), verbose=dict(argstr='-verb'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_files=dict(argstr=' %s', copyfile=False, mandatory=True, position=-1), num_threads=dict(nohash=True, usedefault=True), out_file=dict(argstr='-prefix %s', extensions=None, name_source='in_files', name_template='%s_tcat'), outputtype=dict(), rlt=dict(argstr='-rlt%s', position=1), verbose=dict(argstr='-verb'))
```

## Next Steps


---

*Source: test_auto_TCat.py:6 | Complexity: Beginner | Last updated: 2026-05-18*