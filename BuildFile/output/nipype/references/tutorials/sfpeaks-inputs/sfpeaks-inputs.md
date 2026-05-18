# How To: Sfpeaks Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test SFPeaks inputs

## Prerequisites

**Required Modules:**
- `odf`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), density=dict(argstr='-density %d', units='NA'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-inputfile %s', extensions=None, mandatory=True), inputmodel=dict(argstr='-inputmodel %s', mandatory=True), mepointset=dict(argstr='-mepointset %d', units='NA'), noconsistencycheck=dict(argstr='-noconsistencycheck'), numpds=dict(argstr='-numpds %d', units='NA'), order=dict(argstr='-order %d', units='NA'), out_file=dict(argstr='> %s', extensions=None, genfile=True, position=-1), pdthresh=dict(argstr='-pdthresh %f', units='NA'), pointset=dict(argstr='-pointset %d', units='NA'), rbfpointset=dict(argstr='-rbfpointset %d', units='NA'), scheme_file=dict(argstr='%s', extensions=None), searchradius=dict(argstr='-searchradius %f', units='NA'), stdsfrommean=dict(argstr='-stdsfrommean %f', units='NA'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), density=dict(argstr='-density %d', units='NA'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-inputfile %s', extensions=None, mandatory=True), inputmodel=dict(argstr='-inputmodel %s', mandatory=True), mepointset=dict(argstr='-mepointset %d', units='NA'), noconsistencycheck=dict(argstr='-noconsistencycheck'), numpds=dict(argstr='-numpds %d', units='NA'), order=dict(argstr='-order %d', units='NA'), out_file=dict(argstr='> %s', extensions=None, genfile=True, position=-1), pdthresh=dict(argstr='-pdthresh %f', units='NA'), pointset=dict(argstr='-pointset %d', units='NA'), rbfpointset=dict(argstr='-rbfpointset %d', units='NA'), scheme_file=dict(argstr='%s', extensions=None), searchradius=dict(argstr='-searchradius %f', units='NA'), stdsfrommean=dict(argstr='-stdsfrommean %f', units='NA'))
```

## Next Steps


---

*Source: test_auto_SFPeaks.py:6 | Complexity: Beginner | Last updated: 2026-05-18*