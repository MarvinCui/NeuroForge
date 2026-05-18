# How To: Tca Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Tca inputs

## Prerequisites

**Required Modules:**
- `brainsuite`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), foregroundDelta=dict(argstr='--delta %d', usedefault=True), inputMaskFile=dict(argstr='-i %s', extensions=None, mandatory=True), maxCorrectionSize=dict(argstr='-n %d'), minCorrectionSize=dict(argstr='-m %d', usedefault=True), outputMaskFile=dict(argstr='-o %s', extensions=None, genfile=True), timer=dict(argstr='--timer'), verbosity=dict(argstr='-v %d'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), foregroundDelta=dict(argstr='--delta %d', usedefault=True), inputMaskFile=dict(argstr='-i %s', extensions=None, mandatory=True), maxCorrectionSize=dict(argstr='-n %d'), minCorrectionSize=dict(argstr='-m %d', usedefault=True), outputMaskFile=dict(argstr='-o %s', extensions=None, genfile=True), timer=dict(argstr='--timer'), verbosity=dict(argstr='-v %d'))
```

## Next Steps


---

*Source: test_auto_Tca.py:6 | Complexity: Beginner | Last updated: 2026-05-18*