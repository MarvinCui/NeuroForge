# How To: Jistintensitymp2Ragemasking Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test JistIntensityMp2rageMasking inputs

## Prerequisites

**Required Modules:**
- `developer`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inBackground=dict(argstr='--inBackground %s'), inMasking=dict(argstr='--inMasking %s'), inQuantitative=dict(argstr='--inQuantitative %s', extensions=None), inSecond=dict(argstr='--inSecond %s', extensions=None), inSkip=dict(argstr='--inSkip %s'), inT1weighted=dict(argstr='--inT1weighted %s', extensions=None), null=dict(argstr='--null %s'), outMasked=dict(argstr='--outMasked_T1_Map %s', hash_files=False), outMasked2=dict(argstr='--outMasked_T1weighted %s', hash_files=False), outSignal=dict(argstr='--outSignal_Proba %s', hash_files=False), outSignal2=dict(argstr='--outSignal_Mask %s', hash_files=False), xDefaultMem=dict(argstr='-xDefaultMem %d'), xMaxProcess=dict(argstr='-xMaxProcess %d', usedefault=True), xPrefExt=dict(argstr='--xPrefExt %s'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inBackground=dict(argstr='--inBackground %s'), inMasking=dict(argstr='--inMasking %s'), inQuantitative=dict(argstr='--inQuantitative %s', extensions=None), inSecond=dict(argstr='--inSecond %s', extensions=None), inSkip=dict(argstr='--inSkip %s'), inT1weighted=dict(argstr='--inT1weighted %s', extensions=None), null=dict(argstr='--null %s'), outMasked=dict(argstr='--outMasked_T1_Map %s', hash_files=False), outMasked2=dict(argstr='--outMasked_T1weighted %s', hash_files=False), outSignal=dict(argstr='--outSignal_Proba %s', hash_files=False), outSignal2=dict(argstr='--outSignal_Mask %s', hash_files=False), xDefaultMem=dict(argstr='-xDefaultMem %d'), xMaxProcess=dict(argstr='-xMaxProcess %d', usedefault=True), xPrefExt=dict(argstr='--xPrefExt %s'))
```

## Next Steps


---

*Source: test_auto_JistIntensityMp2rageMasking.py:6 | Complexity: Beginner | Last updated: 2026-05-18*