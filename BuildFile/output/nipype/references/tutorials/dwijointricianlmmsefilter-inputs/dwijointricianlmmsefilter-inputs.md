# How To: Dwijointricianlmmsefilter Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test DWIJointRicianLMMSEFilter inputs

## Prerequisites

**Required Modules:**
- `diffusion`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), compressOutput=dict(argstr='--compressOutput '), environ=dict(nohash=True, usedefault=True), inputVolume=dict(argstr='%s', extensions=None, position=-2), ng=dict(argstr='--ng %d'), outputVolume=dict(argstr='%s', hash_files=False, position=-1), re=dict(argstr='--re %s', sep=','), rf=dict(argstr='--rf %s', sep=','))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), compressOutput=dict(argstr='--compressOutput '), environ=dict(nohash=True, usedefault=True), inputVolume=dict(argstr='%s', extensions=None, position=-2), ng=dict(argstr='--ng %d'), outputVolume=dict(argstr='%s', hash_files=False, position=-1), re=dict(argstr='--re %s', sep=','), rf=dict(argstr='--rf %s', sep=','))
```

## Next Steps


---

*Source: test_auto_DWIJointRicianLMMSEFilter.py:6 | Complexity: Beginner | Last updated: 2026-05-18*