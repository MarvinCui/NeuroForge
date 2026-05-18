# How To: Fim Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Fim inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), fim_thr=dict(argstr='-fim_thr %f', position=3), ideal_file=dict(argstr='-ideal_file %s', extensions=None, mandatory=True, position=2), in_file=dict(argstr='-input %s', copyfile=False, extensions=None, mandatory=True, position=1), num_threads=dict(nohash=True, usedefault=True), out=dict(argstr='-out %s', position=4), out_file=dict(argstr='-bucket %s', extensions=None, name_source='in_file', name_template='%s_fim'), outputtype=dict())
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), fim_thr=dict(argstr='-fim_thr %f', position=3), ideal_file=dict(argstr='-ideal_file %s', extensions=None, mandatory=True, position=2), in_file=dict(argstr='-input %s', copyfile=False, extensions=None, mandatory=True, position=1), num_threads=dict(nohash=True, usedefault=True), out=dict(argstr='-out %s', position=4), out_file=dict(argstr='-bucket %s', extensions=None, name_source='in_file', name_template='%s_fim'), outputtype=dict())
```

## Next Steps


---

*Source: test_auto_Fim.py:6 | Complexity: Beginner | Last updated: 2026-05-18*