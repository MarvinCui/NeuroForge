# How To: Edge3 Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Edge3 inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), datum=dict(argstr='-datum %s'), environ=dict(nohash=True, usedefault=True), fscale=dict(argstr='-fscale', xor=['gscale', 'nscale', 'scale_floats']), gscale=dict(argstr='-gscale', xor=['fscale', 'nscale', 'scale_floats']), in_file=dict(argstr='-input %s', copyfile=False, extensions=None, mandatory=True, position=0), nscale=dict(argstr='-nscale', xor=['fscale', 'gscale', 'scale_floats']), num_threads=dict(nohash=True, usedefault=True), out_file=dict(argstr='-prefix %s', extensions=None, position=-1), outputtype=dict(), scale_floats=dict(argstr='-scale_floats %f', xor=['fscale', 'gscale', 'nscale']), verbose=dict(argstr='-verbose'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), datum=dict(argstr='-datum %s'), environ=dict(nohash=True, usedefault=True), fscale=dict(argstr='-fscale', xor=['gscale', 'nscale', 'scale_floats']), gscale=dict(argstr='-gscale', xor=['fscale', 'nscale', 'scale_floats']), in_file=dict(argstr='-input %s', copyfile=False, extensions=None, mandatory=True, position=0), nscale=dict(argstr='-nscale', xor=['fscale', 'gscale', 'scale_floats']), num_threads=dict(nohash=True, usedefault=True), out_file=dict(argstr='-prefix %s', extensions=None, position=-1), outputtype=dict(), scale_floats=dict(argstr='-scale_floats %f', xor=['fscale', 'gscale', 'nscale']), verbose=dict(argstr='-verbose'))
```

## Next Steps


---

*Source: test_auto_Edge3.py:6 | Complexity: Beginner | Last updated: 2026-05-18*