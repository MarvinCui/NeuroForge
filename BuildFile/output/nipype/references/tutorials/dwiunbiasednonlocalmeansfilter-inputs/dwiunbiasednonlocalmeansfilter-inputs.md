# How To: Dwiunbiasednonlocalmeansfilter Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test DWIUnbiasedNonLocalMeansFilter inputs

## Prerequisites

**Required Modules:**
- `denoising`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), hp=dict(argstr='--hp %f'), inputVolume=dict(argstr='%s', extensions=None, position=-2), ng=dict(argstr='--ng %d'), outputVolume=dict(argstr='%s', hash_files=False, position=-1), rc=dict(argstr='--rc %s', sep=','), re=dict(argstr='--re %s', sep=','), rs=dict(argstr='--rs %s', sep=','))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), hp=dict(argstr='--hp %f'), inputVolume=dict(argstr='%s', extensions=None, position=-2), ng=dict(argstr='--ng %d'), outputVolume=dict(argstr='%s', hash_files=False, position=-1), rc=dict(argstr='--rc %s', sep=','), re=dict(argstr='--re %s', sep=','), rs=dict(argstr='--rs %s', sep=','))
```

## Next Steps


---

*Source: test_auto_DWIUnbiasedNonLocalMeansFilter.py:6 | Complexity: Beginner | Last updated: 2026-05-18*