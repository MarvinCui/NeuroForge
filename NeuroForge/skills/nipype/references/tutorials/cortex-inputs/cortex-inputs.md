# How To: Cortex Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Cortex inputs

## Prerequisites

**Required Modules:**
- `brainsuite`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), computeGCBoundary=dict(argstr='-g'), computeWGBoundary=dict(argstr='-w', usedefault=True), environ=dict(nohash=True, usedefault=True), includeAllSubcorticalAreas=dict(argstr='-a', usedefault=True), inputHemisphereLabelFile=dict(argstr='-h %s', extensions=None, mandatory=True), inputTissueFractionFile=dict(argstr='-f %s', extensions=None, mandatory=True), outputCerebrumMask=dict(argstr='-o %s', extensions=None, genfile=True), timer=dict(argstr='--timer'), tissueFractionThreshold=dict(argstr='-p %f', usedefault=True), verbosity=dict(argstr='-v %d'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), computeGCBoundary=dict(argstr='-g'), computeWGBoundary=dict(argstr='-w', usedefault=True), environ=dict(nohash=True, usedefault=True), includeAllSubcorticalAreas=dict(argstr='-a', usedefault=True), inputHemisphereLabelFile=dict(argstr='-h %s', extensions=None, mandatory=True), inputTissueFractionFile=dict(argstr='-f %s', extensions=None, mandatory=True), outputCerebrumMask=dict(argstr='-o %s', extensions=None, genfile=True), timer=dict(argstr='--timer'), tissueFractionThreshold=dict(argstr='-p %f', usedefault=True), verbosity=dict(argstr='-v %d'))
```

## Next Steps


---

*Source: test_auto_Cortex.py:6 | Complexity: Beginner | Last updated: 2026-05-18*