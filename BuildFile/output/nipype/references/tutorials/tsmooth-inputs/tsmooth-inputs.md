# How To: Tsmooth Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test TSmooth inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(adaptive=dict(argstr='-adaptive %d'), args=dict(argstr='%s'), blackman=dict(argstr='-blackman %d'), custom=dict(argstr='-custom %s', extensions=None), datum=dict(argstr='-datum %s'), environ=dict(nohash=True, usedefault=True), hamming=dict(argstr='-hamming %d'), in_file=dict(argstr='%s', copyfile=False, extensions=None, mandatory=True, position=-1), lin=dict(argstr='-lin'), lin3=dict(argstr='-3lin %d'), med=dict(argstr='-med'), num_threads=dict(nohash=True, usedefault=True), osf=dict(argstr='-osf'), out_file=dict(argstr='-prefix %s', extensions=None, name_source='in_file', name_template='%s_smooth'), outputtype=dict())
```


## Complete Example

```python
# Workflow
input_map = dict(adaptive=dict(argstr='-adaptive %d'), args=dict(argstr='%s'), blackman=dict(argstr='-blackman %d'), custom=dict(argstr='-custom %s', extensions=None), datum=dict(argstr='-datum %s'), environ=dict(nohash=True, usedefault=True), hamming=dict(argstr='-hamming %d'), in_file=dict(argstr='%s', copyfile=False, extensions=None, mandatory=True, position=-1), lin=dict(argstr='-lin'), lin3=dict(argstr='-3lin %d'), med=dict(argstr='-med'), num_threads=dict(nohash=True, usedefault=True), osf=dict(argstr='-osf'), out_file=dict(argstr='-prefix %s', extensions=None, name_source='in_file', name_template='%s_smooth'), outputtype=dict())
```

## Next Steps


---

*Source: test_auto_TSmooth.py:6 | Complexity: Beginner | Last updated: 2026-05-18*