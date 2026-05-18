# How To: Catmatvec Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test CatMatvec inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), fourxfour=dict(argstr='-4x4', xor=['matrix', 'oneline']), in_file=dict(argstr='%s', mandatory=True, position=-2), matrix=dict(argstr='-MATRIX', xor=['oneline', 'fourxfour']), num_threads=dict(nohash=True, usedefault=True), oneline=dict(argstr='-ONELINE', xor=['matrix', 'fourxfour']), out_file=dict(argstr=' > %s', extensions=None, keep_extension=False, mandatory=True, name_source='in_file', name_template='%s_cat.aff12.1D', position=-1), outputtype=dict())
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), fourxfour=dict(argstr='-4x4', xor=['matrix', 'oneline']), in_file=dict(argstr='%s', mandatory=True, position=-2), matrix=dict(argstr='-MATRIX', xor=['oneline', 'fourxfour']), num_threads=dict(nohash=True, usedefault=True), oneline=dict(argstr='-ONELINE', xor=['matrix', 'fourxfour']), out_file=dict(argstr=' > %s', extensions=None, keep_extension=False, mandatory=True, name_source='in_file', name_template='%s_cat.aff12.1D', position=-1), outputtype=dict())
```

## Next Steps


---

*Source: test_auto_CatMatvec.py:6 | Complexity: Beginner | Last updated: 2026-05-18*