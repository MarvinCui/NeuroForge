# How To: Createjacobiandeterminantimage Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test CreateJacobianDeterminantImage inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), deformationField=dict(argstr='%s', extensions=None, mandatory=True, position=1), doLogJacobian=dict(argstr='%d', position=3), environ=dict(nohash=True, usedefault=True), imageDimension=dict(argstr='%d', mandatory=True, position=0), num_threads=dict(nohash=True, usedefault=True), outputImage=dict(argstr='%s', extensions=None, mandatory=True, position=2), useGeometric=dict(argstr='%d', position=4))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), deformationField=dict(argstr='%s', extensions=None, mandatory=True, position=1), doLogJacobian=dict(argstr='%d', position=3), environ=dict(nohash=True, usedefault=True), imageDimension=dict(argstr='%d', mandatory=True, position=0), num_threads=dict(nohash=True, usedefault=True), outputImage=dict(argstr='%s', extensions=None, mandatory=True, position=2), useGeometric=dict(argstr='%d', position=4))
```

## Next Steps


---

*Source: test_auto_CreateJacobianDeterminantImage.py:6 | Complexity: Beginner | Last updated: 2026-05-18*