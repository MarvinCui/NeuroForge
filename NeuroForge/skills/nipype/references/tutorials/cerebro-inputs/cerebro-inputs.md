# How To: Cerebro Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Cerebro inputs

## Prerequisites

**Required Modules:**
- `brainsuite`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), costFunction=dict(argstr='-c %d', usedefault=True), environ=dict(nohash=True, usedefault=True), inputAtlasLabelFile=dict(argstr='--atlaslabels %s', extensions=None, mandatory=True), inputAtlasMRIFile=dict(argstr='--atlas %s', extensions=None, mandatory=True), inputBrainMaskFile=dict(argstr='-m %s', extensions=None), inputMRIFile=dict(argstr='-i %s', extensions=None, mandatory=True), keepTempFiles=dict(argstr='--keep'), linearConvergence=dict(argstr='--linconv %f'), outputAffineTransformFile=dict(argstr='--air %s', extensions=None, genfile=True), outputCerebrumMaskFile=dict(argstr='-o %s', extensions=None, genfile=True), outputLabelVolumeFile=dict(argstr='-l %s', extensions=None, genfile=True), outputWarpTransformFile=dict(argstr='--warp %s', extensions=None, genfile=True), tempDirectory=dict(argstr='--tempdir %s'), tempDirectoryBase=dict(argstr='--tempdirbase %s'), useCentroids=dict(argstr='--centroids'), verbosity=dict(argstr='-v %d'), warpConvergence=dict(argstr='--warpconv %f'), warpLabel=dict(argstr='--warplevel %d'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), costFunction=dict(argstr='-c %d', usedefault=True), environ=dict(nohash=True, usedefault=True), inputAtlasLabelFile=dict(argstr='--atlaslabels %s', extensions=None, mandatory=True), inputAtlasMRIFile=dict(argstr='--atlas %s', extensions=None, mandatory=True), inputBrainMaskFile=dict(argstr='-m %s', extensions=None), inputMRIFile=dict(argstr='-i %s', extensions=None, mandatory=True), keepTempFiles=dict(argstr='--keep'), linearConvergence=dict(argstr='--linconv %f'), outputAffineTransformFile=dict(argstr='--air %s', extensions=None, genfile=True), outputCerebrumMaskFile=dict(argstr='-o %s', extensions=None, genfile=True), outputLabelVolumeFile=dict(argstr='-l %s', extensions=None, genfile=True), outputWarpTransformFile=dict(argstr='--warp %s', extensions=None, genfile=True), tempDirectory=dict(argstr='--tempdir %s'), tempDirectoryBase=dict(argstr='--tempdirbase %s'), useCentroids=dict(argstr='--centroids'), verbosity=dict(argstr='-v %d'), warpConvergence=dict(argstr='--warpconv %f'), warpLabel=dict(argstr='--warplevel %d'))
```

## Next Steps


---

*Source: test_auto_Cerebro.py:6 | Complexity: Beginner | Last updated: 2026-05-18*