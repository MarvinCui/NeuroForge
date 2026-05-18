# How To: Bse Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Bse inputs

## Prerequisites

**Required Modules:**
- `brainsuite`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), diffusionConstant=dict(argstr='-d %f', usedefault=True), diffusionIterations=dict(argstr='-n %d', usedefault=True), dilateFinalMask=dict(argstr='-p', usedefault=True), edgeDetectionConstant=dict(argstr='-s %f', usedefault=True), environ=dict(nohash=True, usedefault=True), inputMRIFile=dict(argstr='-i %s', extensions=None, mandatory=True), noRotate=dict(argstr='--norotate'), outputCortexFile=dict(argstr='--cortex %s', extensions=None, hash_files=False), outputDetailedBrainMask=dict(argstr='--hires %s', extensions=None, hash_files=False), outputDiffusionFilter=dict(argstr='--adf %s', extensions=None, hash_files=False), outputEdgeMap=dict(argstr='--edge %s', extensions=None, hash_files=False), outputMRIVolume=dict(argstr='-o %s', extensions=None, genfile=True, hash_files=False), outputMaskFile=dict(argstr='--mask %s', extensions=None, genfile=True, hash_files=False), radius=dict(argstr='-r %f', usedefault=True), timer=dict(argstr='--timer'), trim=dict(argstr='--trim', usedefault=True), verbosityLevel=dict(argstr='-v %f', usedefault=True))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), diffusionConstant=dict(argstr='-d %f', usedefault=True), diffusionIterations=dict(argstr='-n %d', usedefault=True), dilateFinalMask=dict(argstr='-p', usedefault=True), edgeDetectionConstant=dict(argstr='-s %f', usedefault=True), environ=dict(nohash=True, usedefault=True), inputMRIFile=dict(argstr='-i %s', extensions=None, mandatory=True), noRotate=dict(argstr='--norotate'), outputCortexFile=dict(argstr='--cortex %s', extensions=None, hash_files=False), outputDetailedBrainMask=dict(argstr='--hires %s', extensions=None, hash_files=False), outputDiffusionFilter=dict(argstr='--adf %s', extensions=None, hash_files=False), outputEdgeMap=dict(argstr='--edge %s', extensions=None, hash_files=False), outputMRIVolume=dict(argstr='-o %s', extensions=None, genfile=True, hash_files=False), outputMaskFile=dict(argstr='--mask %s', extensions=None, genfile=True, hash_files=False), radius=dict(argstr='-r %f', usedefault=True), timer=dict(argstr='--timer'), trim=dict(argstr='--trim', usedefault=True), verbosityLevel=dict(argstr='-v %f', usedefault=True))
```

## Next Steps


---

*Source: test_auto_Bse.py:6 | Complexity: Beginner | Last updated: 2026-05-18*