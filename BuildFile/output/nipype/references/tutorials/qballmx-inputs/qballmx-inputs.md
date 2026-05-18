# How To: Qballmx Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test QBallMX inputs

## Prerequisites

**Required Modules:**
- `odf`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), basistype=dict(argstr='-basistype %s', usedefault=True), environ=dict(nohash=True, usedefault=True), order=dict(argstr='-order %d', units='NA'), out_file=dict(argstr='> %s', extensions=None, genfile=True, position=-1), rbfpointset=dict(argstr='-rbfpointset %d', units='NA'), rbfsigma=dict(argstr='-rbfsigma %f', units='NA'), scheme_file=dict(argstr='-schemefile %s', extensions=None, mandatory=True), smoothingsigma=dict(argstr='-smoothingsigma %f', units='NA'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), basistype=dict(argstr='-basistype %s', usedefault=True), environ=dict(nohash=True, usedefault=True), order=dict(argstr='-order %d', units='NA'), out_file=dict(argstr='> %s', extensions=None, genfile=True, position=-1), rbfpointset=dict(argstr='-rbfpointset %d', units='NA'), rbfsigma=dict(argstr='-rbfsigma %f', units='NA'), scheme_file=dict(argstr='-schemefile %s', extensions=None, mandatory=True), smoothingsigma=dict(argstr='-smoothingsigma %f', units='NA'))
```

## Next Steps


---

*Source: test_auto_QBallMX.py:6 | Complexity: Beginner | Last updated: 2026-05-18*