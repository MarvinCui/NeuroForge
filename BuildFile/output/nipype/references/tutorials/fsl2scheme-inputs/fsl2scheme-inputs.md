# How To: Fsl2Scheme Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test FSL2Scheme inputs

## Prerequisites

**Required Modules:**
- `convert`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), bscale=dict(argstr='-bscale %d', units='NA'), bval_file=dict(argstr='-bvalfile %s', extensions=None, mandatory=True, position=2), bvec_file=dict(argstr='-bvecfile %s', extensions=None, mandatory=True, position=1), diffusiontime=dict(argstr='-diffusiontime %f', units='NA'), environ=dict(nohash=True, usedefault=True), flipx=dict(argstr='-flipx'), flipy=dict(argstr='-flipy'), flipz=dict(argstr='-flipz'), interleave=dict(argstr='-interleave'), numscans=dict(argstr='-numscans %d', units='NA'), out_file=dict(argstr='> %s', extensions=None, genfile=True, position=-1), usegradmod=dict(argstr='-usegradmod'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), bscale=dict(argstr='-bscale %d', units='NA'), bval_file=dict(argstr='-bvalfile %s', extensions=None, mandatory=True, position=2), bvec_file=dict(argstr='-bvecfile %s', extensions=None, mandatory=True, position=1), diffusiontime=dict(argstr='-diffusiontime %f', units='NA'), environ=dict(nohash=True, usedefault=True), flipx=dict(argstr='-flipx'), flipy=dict(argstr='-flipy'), flipz=dict(argstr='-flipz'), interleave=dict(argstr='-interleave'), numscans=dict(argstr='-numscans %d', units='NA'), out_file=dict(argstr='> %s', extensions=None, genfile=True, position=-1), usegradmod=dict(argstr='-usegradmod'))
```

## Next Steps


---

*Source: test_auto_FSL2Scheme.py:6 | Complexity: Beginner | Last updated: 2026-05-18*