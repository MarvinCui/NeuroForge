# How To: Jistbrainmp2Rageduraestimation Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test JistBrainMp2rageDuraEstimation inputs

## Prerequisites

**Required Modules:**
- `developer`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inDistance=dict(argstr='--inDistance %f'), inSecond=dict(argstr='--inSecond %s', extensions=None), inSkull=dict(argstr='--inSkull %s', extensions=None), inoutput=dict(argstr='--inoutput %s'), null=dict(argstr='--null %s'), outDura=dict(argstr='--outDura %s', hash_files=False), xDefaultMem=dict(argstr='-xDefaultMem %d'), xMaxProcess=dict(argstr='-xMaxProcess %d', usedefault=True), xPrefExt=dict(argstr='--xPrefExt %s'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inDistance=dict(argstr='--inDistance %f'), inSecond=dict(argstr='--inSecond %s', extensions=None), inSkull=dict(argstr='--inSkull %s', extensions=None), inoutput=dict(argstr='--inoutput %s'), null=dict(argstr='--null %s'), outDura=dict(argstr='--outDura %s', hash_files=False), xDefaultMem=dict(argstr='-xDefaultMem %d'), xMaxProcess=dict(argstr='-xMaxProcess %d', usedefault=True), xPrefExt=dict(argstr='--xPrefExt %s'))
```

## Next Steps


---

*Source: test_auto_JistBrainMp2rageDuraEstimation.py:6 | Complexity: Beginner | Last updated: 2026-05-18*