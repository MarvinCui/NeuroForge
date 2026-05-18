# How To: Pvc Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Pvc inputs

## Prerequisites

**Required Modules:**
- `brainsuite`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputMRIFile=dict(argstr='-i %s', extensions=None, mandatory=True), inputMaskFile=dict(argstr='-m %s', extensions=None), outputLabelFile=dict(argstr='-o %s', extensions=None, genfile=True), outputTissueFractionFile=dict(argstr='-f %s', extensions=None, genfile=True), spatialPrior=dict(argstr='-l %f'), threeClassFlag=dict(argstr='-3'), timer=dict(argstr='--timer'), verbosity=dict(argstr='-v %d'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputMRIFile=dict(argstr='-i %s', extensions=None, mandatory=True), inputMaskFile=dict(argstr='-m %s', extensions=None), outputLabelFile=dict(argstr='-o %s', extensions=None, genfile=True), outputTissueFractionFile=dict(argstr='-f %s', extensions=None, genfile=True), spatialPrior=dict(argstr='-l %f'), threeClassFlag=dict(argstr='-3'), timer=dict(argstr='--timer'), verbosity=dict(argstr='-v %d'))
```

## Next Steps


---

*Source: test_auto_Pvc.py:6 | Complexity: Beginner | Last updated: 2026-05-18*