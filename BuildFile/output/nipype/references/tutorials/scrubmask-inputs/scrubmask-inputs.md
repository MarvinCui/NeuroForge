# How To: Scrubmask Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Scrubmask inputs

## Prerequisites

**Required Modules:**
- `brainsuite`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), backgroundFillThreshold=dict(argstr='-b %d', usedefault=True), environ=dict(nohash=True, usedefault=True), foregroundTrimThreshold=dict(argstr='-f %d', usedefault=True), inputMaskFile=dict(argstr='-i %s', extensions=None, mandatory=True), numberIterations=dict(argstr='-n %d'), outputMaskFile=dict(argstr='-o %s', extensions=None, genfile=True), timer=dict(argstr='--timer'), verbosity=dict(argstr='-v %d'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), backgroundFillThreshold=dict(argstr='-b %d', usedefault=True), environ=dict(nohash=True, usedefault=True), foregroundTrimThreshold=dict(argstr='-f %d', usedefault=True), inputMaskFile=dict(argstr='-i %s', extensions=None, mandatory=True), numberIterations=dict(argstr='-n %d'), outputMaskFile=dict(argstr='-o %s', extensions=None, genfile=True), timer=dict(argstr='--timer'), verbosity=dict(argstr='-v %d'))
```

## Next Steps


---

*Source: test_auto_Scrubmask.py:6 | Complexity: Beginner | Last updated: 2026-05-18*