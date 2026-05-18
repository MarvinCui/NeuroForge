# How To: Skullfinder Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Skullfinder inputs

## Prerequisites

**Required Modules:**
- `brainsuite`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), bgLabelValue=dict(argstr='--bglabel %d'), brainLabelValue=dict(argstr='--brainlabel %d'), environ=dict(nohash=True, usedefault=True), inputMRIFile=dict(argstr='-i %s', extensions=None, mandatory=True), inputMaskFile=dict(argstr='-m %s', extensions=None, mandatory=True), lowerThreshold=dict(argstr='-l %d'), outputLabelFile=dict(argstr='-o %s', extensions=None, genfile=True), performFinalOpening=dict(argstr='--finalOpening'), scalpLabelValue=dict(argstr='--scalplabel %d'), skullLabelValue=dict(argstr='--skulllabel %d'), spaceLabelValue=dict(argstr='--spacelabel %d'), surfaceFilePrefix=dict(argstr='-s %s'), upperThreshold=dict(argstr='-u %d'), verbosity=dict(argstr='-v %d'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), bgLabelValue=dict(argstr='--bglabel %d'), brainLabelValue=dict(argstr='--brainlabel %d'), environ=dict(nohash=True, usedefault=True), inputMRIFile=dict(argstr='-i %s', extensions=None, mandatory=True), inputMaskFile=dict(argstr='-m %s', extensions=None, mandatory=True), lowerThreshold=dict(argstr='-l %d'), outputLabelFile=dict(argstr='-o %s', extensions=None, genfile=True), performFinalOpening=dict(argstr='--finalOpening'), scalpLabelValue=dict(argstr='--scalplabel %d'), skullLabelValue=dict(argstr='--skulllabel %d'), spaceLabelValue=dict(argstr='--spacelabel %d'), surfaceFilePrefix=dict(argstr='-s %s'), upperThreshold=dict(argstr='-u %d'), verbosity=dict(argstr='-v %d'))
```

## Next Steps


---

*Source: test_auto_Skullfinder.py:6 | Complexity: Beginner | Last updated: 2026-05-18*