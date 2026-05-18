# How To: Aboverlap Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test ABoverlap inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file_a=dict(argstr='%s', copyfile=False, extensions=None, mandatory=True, position=-3), in_file_b=dict(argstr='%s', copyfile=False, extensions=None, mandatory=True, position=-2), no_automask=dict(argstr='-no_automask'), num_threads=dict(nohash=True, usedefault=True), out_file=dict(argstr=' |& tee %s', extensions=None, position=-1), outputtype=dict(), quiet=dict(argstr='-quiet'), verb=dict(argstr='-verb'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file_a=dict(argstr='%s', copyfile=False, extensions=None, mandatory=True, position=-3), in_file_b=dict(argstr='%s', copyfile=False, extensions=None, mandatory=True, position=-2), no_automask=dict(argstr='-no_automask'), num_threads=dict(nohash=True, usedefault=True), out_file=dict(argstr=' |& tee %s', extensions=None, position=-1), outputtype=dict(), quiet=dict(argstr='-quiet'), verb=dict(argstr='-verb'))
```

## Next Steps


---

*Source: test_auto_ABoverlap.py:6 | Complexity: Beginner | Last updated: 2026-05-18*