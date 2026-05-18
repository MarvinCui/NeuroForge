# How To: Jistbrainmgdmsegmentation Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test JistBrainMgdmSegmentation inputs

## Prerequisites

**Required Modules:**
- `developer`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inAdjust=dict(argstr='--inAdjust %s'), inAtlas=dict(argstr='--inAtlas %s', extensions=None), inCompute=dict(argstr='--inCompute %s'), inCurvature=dict(argstr='--inCurvature %f'), inData=dict(argstr='--inData %f'), inFLAIR=dict(argstr='--inFLAIR %s', extensions=None), inMP2RAGE=dict(argstr='--inMP2RAGE %s', extensions=None), inMP2RAGE2=dict(argstr='--inMP2RAGE2 %s', extensions=None), inMPRAGE=dict(argstr='--inMPRAGE %s', extensions=None), inMax=dict(argstr='--inMax %d'), inMin=dict(argstr='--inMin %f'), inOutput=dict(argstr='--inOutput %s'), inPV=dict(argstr='--inPV %s', extensions=None), inPosterior=dict(argstr='--inPosterior %f'), inSteps=dict(argstr='--inSteps %d'), inTopology=dict(argstr='--inTopology %s'), null=dict(argstr='--null %s'), outLevelset=dict(argstr='--outLevelset %s', hash_files=False), outPosterior2=dict(argstr='--outPosterior2 %s', hash_files=False), outPosterior3=dict(argstr='--outPosterior3 %s', hash_files=False), outSegmented=dict(argstr='--outSegmented %s', hash_files=False), xDefaultMem=dict(argstr='-xDefaultMem %d'), xMaxProcess=dict(argstr='-xMaxProcess %d', usedefault=True), xPrefExt=dict(argstr='--xPrefExt %s'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inAdjust=dict(argstr='--inAdjust %s'), inAtlas=dict(argstr='--inAtlas %s', extensions=None), inCompute=dict(argstr='--inCompute %s'), inCurvature=dict(argstr='--inCurvature %f'), inData=dict(argstr='--inData %f'), inFLAIR=dict(argstr='--inFLAIR %s', extensions=None), inMP2RAGE=dict(argstr='--inMP2RAGE %s', extensions=None), inMP2RAGE2=dict(argstr='--inMP2RAGE2 %s', extensions=None), inMPRAGE=dict(argstr='--inMPRAGE %s', extensions=None), inMax=dict(argstr='--inMax %d'), inMin=dict(argstr='--inMin %f'), inOutput=dict(argstr='--inOutput %s'), inPV=dict(argstr='--inPV %s', extensions=None), inPosterior=dict(argstr='--inPosterior %f'), inSteps=dict(argstr='--inSteps %d'), inTopology=dict(argstr='--inTopology %s'), null=dict(argstr='--null %s'), outLevelset=dict(argstr='--outLevelset %s', hash_files=False), outPosterior2=dict(argstr='--outPosterior2 %s', hash_files=False), outPosterior3=dict(argstr='--outPosterior3 %s', hash_files=False), outSegmented=dict(argstr='--outSegmented %s', hash_files=False), xDefaultMem=dict(argstr='-xDefaultMem %d'), xMaxProcess=dict(argstr='-xMaxProcess %d', usedefault=True), xPrefExt=dict(argstr='--xPrefExt %s'))
```

## Next Steps


---

*Source: test_auto_JistBrainMgdmSegmentation.py:6 | Complexity: Beginner | Last updated: 2026-05-18*