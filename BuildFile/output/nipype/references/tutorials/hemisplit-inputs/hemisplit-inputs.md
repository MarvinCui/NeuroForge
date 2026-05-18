# How To: Hemisplit Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Hemisplit inputs

## Prerequisites

**Required Modules:**
- `brainsuite`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputHemisphereLabelFile=dict(argstr='-l %s', extensions=None, mandatory=True), inputSurfaceFile=dict(argstr='-i %s', extensions=None, mandatory=True), outputLeftHemisphere=dict(argstr='--left %s', extensions=None, genfile=True), outputLeftPialHemisphere=dict(argstr='-pl %s', extensions=None, genfile=True), outputRightHemisphere=dict(argstr='--right %s', extensions=None, genfile=True), outputRightPialHemisphere=dict(argstr='-pr %s', extensions=None, genfile=True), pialSurfaceFile=dict(argstr='-p %s', extensions=None), timer=dict(argstr='--timer'), verbosity=dict(argstr='-v %d'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputHemisphereLabelFile=dict(argstr='-l %s', extensions=None, mandatory=True), inputSurfaceFile=dict(argstr='-i %s', extensions=None, mandatory=True), outputLeftHemisphere=dict(argstr='--left %s', extensions=None, genfile=True), outputLeftPialHemisphere=dict(argstr='-pl %s', extensions=None, genfile=True), outputRightHemisphere=dict(argstr='--right %s', extensions=None, genfile=True), outputRightPialHemisphere=dict(argstr='-pr %s', extensions=None, genfile=True), pialSurfaceFile=dict(argstr='-p %s', extensions=None), timer=dict(argstr='--timer'), verbosity=dict(argstr='-v %d'))
```

## Next Steps


---

*Source: test_auto_Hemisplit.py:6 | Complexity: Beginner | Last updated: 2026-05-18*