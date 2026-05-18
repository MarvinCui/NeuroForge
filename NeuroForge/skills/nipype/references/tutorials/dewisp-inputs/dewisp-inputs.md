# How To: Dewisp Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Dewisp inputs

## Prerequisites

**Required Modules:**
- `brainsuite`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputMaskFile=dict(argstr='-i %s', extensions=None, mandatory=True), maximumIterations=dict(argstr='-n %d'), outputMaskFile=dict(argstr='-o %s', extensions=None, genfile=True), sizeThreshold=dict(argstr='-t %d'), timer=dict(argstr='--timer'), verbosity=dict(argstr='-v %d'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputMaskFile=dict(argstr='-i %s', extensions=None, mandatory=True), maximumIterations=dict(argstr='-n %d'), outputMaskFile=dict(argstr='-o %s', extensions=None, genfile=True), sizeThreshold=dict(argstr='-t %d'), timer=dict(argstr='--timer'), verbosity=dict(argstr='-v %d'))
```

## Next Steps


---

*Source: test_auto_Dewisp.py:6 | Complexity: Beginner | Last updated: 2026-05-18*