# How To: Zcat Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Zcat inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), datum=dict(argstr='-datum %s'), environ=dict(nohash=True, usedefault=True), fscale=dict(argstr='-fscale', xor=['nscale']), in_files=dict(argstr='%s', copyfile=False, mandatory=True, position=-1), nscale=dict(argstr='-nscale', xor=['fscale']), num_threads=dict(nohash=True, usedefault=True), out_file=dict(argstr='-prefix %s', extensions=None, name_source='in_files', name_template='%s_zcat'), outputtype=dict(), verb=dict(argstr='-verb'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), datum=dict(argstr='-datum %s'), environ=dict(nohash=True, usedefault=True), fscale=dict(argstr='-fscale', xor=['nscale']), in_files=dict(argstr='%s', copyfile=False, mandatory=True, position=-1), nscale=dict(argstr='-nscale', xor=['fscale']), num_threads=dict(nohash=True, usedefault=True), out_file=dict(argstr='-prefix %s', extensions=None, name_source='in_files', name_template='%s_zcat'), outputtype=dict(), verb=dict(argstr='-verb'))
```

## Next Steps


---

*Source: test_auto_Zcat.py:6 | Complexity: Beginner | Last updated: 2026-05-18*