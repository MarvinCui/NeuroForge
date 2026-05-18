# How To: Jistbrainmp2Rageskullstripping Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test JistBrainMp2rageSkullStripping inputs

## Prerequisites

**Required Modules:**
- `developer`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inFilter=dict(argstr='--inFilter %s', extensions=None), inSecond=dict(argstr='--inSecond %s', extensions=None), inSkip=dict(argstr='--inSkip %s'), inT1=dict(argstr='--inT1 %s', extensions=None), inT1weighted=dict(argstr='--inT1weighted %s', extensions=None), null=dict(argstr='--null %s'), outBrain=dict(argstr='--outBrain %s', hash_files=False), outMasked=dict(argstr='--outMasked %s', hash_files=False), outMasked2=dict(argstr='--outMasked2 %s', hash_files=False), outMasked3=dict(argstr='--outMasked3 %s', hash_files=False), xDefaultMem=dict(argstr='-xDefaultMem %d'), xMaxProcess=dict(argstr='-xMaxProcess %d', usedefault=True), xPrefExt=dict(argstr='--xPrefExt %s'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inFilter=dict(argstr='--inFilter %s', extensions=None), inSecond=dict(argstr='--inSecond %s', extensions=None), inSkip=dict(argstr='--inSkip %s'), inT1=dict(argstr='--inT1 %s', extensions=None), inT1weighted=dict(argstr='--inT1weighted %s', extensions=None), null=dict(argstr='--null %s'), outBrain=dict(argstr='--outBrain %s', hash_files=False), outMasked=dict(argstr='--outMasked %s', hash_files=False), outMasked2=dict(argstr='--outMasked2 %s', hash_files=False), outMasked3=dict(argstr='--outMasked3 %s', hash_files=False), xDefaultMem=dict(argstr='-xDefaultMem %d'), xMaxProcess=dict(argstr='-xMaxProcess %d', usedefault=True), xPrefExt=dict(argstr='--xPrefExt %s'))
```

## Next Steps


---

*Source: test_auto_JistBrainMp2rageSkullStripping.py:6 | Complexity: Beginner | Last updated: 2026-05-18*