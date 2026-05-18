# How To: Dwiricianlmmsefilter Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test DWIRicianLMMSEFilter inputs

## Prerequisites

**Required Modules:**
- `diffusion`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), compressOutput=dict(argstr='--compressOutput '), environ=dict(nohash=True, usedefault=True), hrf=dict(argstr='--hrf %f'), inputVolume=dict(argstr='%s', extensions=None, position=-2), iter=dict(argstr='--iter %d'), maxnstd=dict(argstr='--maxnstd %d'), minnstd=dict(argstr='--minnstd %d'), mnve=dict(argstr='--mnve %d'), mnvf=dict(argstr='--mnvf %d'), outputVolume=dict(argstr='%s', hash_files=False, position=-1), re=dict(argstr='--re %s', sep=','), rf=dict(argstr='--rf %s', sep=','), uav=dict(argstr='--uav '))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), compressOutput=dict(argstr='--compressOutput '), environ=dict(nohash=True, usedefault=True), hrf=dict(argstr='--hrf %f'), inputVolume=dict(argstr='%s', extensions=None, position=-2), iter=dict(argstr='--iter %d'), maxnstd=dict(argstr='--maxnstd %d'), minnstd=dict(argstr='--minnstd %d'), mnve=dict(argstr='--mnve %d'), mnvf=dict(argstr='--mnvf %d'), outputVolume=dict(argstr='%s', hash_files=False, position=-1), re=dict(argstr='--re %s', sep=','), rf=dict(argstr='--rf %s', sep=','), uav=dict(argstr='--uav '))
```

## Next Steps


---

*Source: test_auto_DWIRicianLMMSEFilter.py:6 | Complexity: Beginner | Last updated: 2026-05-18*