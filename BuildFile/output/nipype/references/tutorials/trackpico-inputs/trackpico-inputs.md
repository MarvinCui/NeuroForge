# How To: Trackpico Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test TrackPICo inputs

## Prerequisites

**Required Modules:**
- `dti`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(anisfile=dict(argstr='-anisfile %s', extensions=None), anisthresh=dict(argstr='-anisthresh %f'), args=dict(argstr='%s'), curveinterval=dict(argstr='-curveinterval %f', requires=['curvethresh']), curvethresh=dict(argstr='-curvethresh %f'), data_dims=dict(argstr='-datadims %s', units='voxels'), environ=dict(nohash=True, usedefault=True), gzip=dict(argstr='-gzip'), in_file=dict(argstr='-inputfile %s', extensions=None, position=1), inputdatatype=dict(argstr='-inputdatatype %s'), inputmodel=dict(argstr='-inputmodel %s', usedefault=True), interpolator=dict(argstr='-interpolator %s'), ipthresh=dict(argstr='-ipthresh %f'), iterations=dict(argstr='-iterations %d', units='NA'), maxcomponents=dict(argstr='-maxcomponents %d', units='NA'), numpds=dict(argstr='-numpds %d', units='NA'), out_file=dict(argstr='-outputfile %s', extensions=None, genfile=True, position=-1), output_root=dict(argstr='-outputroot %s', extensions=None, position=-1), outputtracts=dict(argstr='-outputtracts %s'), pdf=dict(argstr='-pdf %s'), seed_file=dict(argstr='-seedfile %s', extensions=None, position=2), stepsize=dict(argstr='-stepsize %f', requires=['tracker']), tracker=dict(argstr='-tracker %s', usedefault=True), voxel_dims=dict(argstr='-voxeldims %s', units='mm'))
```


## Complete Example

```python
# Workflow
input_map = dict(anisfile=dict(argstr='-anisfile %s', extensions=None), anisthresh=dict(argstr='-anisthresh %f'), args=dict(argstr='%s'), curveinterval=dict(argstr='-curveinterval %f', requires=['curvethresh']), curvethresh=dict(argstr='-curvethresh %f'), data_dims=dict(argstr='-datadims %s', units='voxels'), environ=dict(nohash=True, usedefault=True), gzip=dict(argstr='-gzip'), in_file=dict(argstr='-inputfile %s', extensions=None, position=1), inputdatatype=dict(argstr='-inputdatatype %s'), inputmodel=dict(argstr='-inputmodel %s', usedefault=True), interpolator=dict(argstr='-interpolator %s'), ipthresh=dict(argstr='-ipthresh %f'), iterations=dict(argstr='-iterations %d', units='NA'), maxcomponents=dict(argstr='-maxcomponents %d', units='NA'), numpds=dict(argstr='-numpds %d', units='NA'), out_file=dict(argstr='-outputfile %s', extensions=None, genfile=True, position=-1), output_root=dict(argstr='-outputroot %s', extensions=None, position=-1), outputtracts=dict(argstr='-outputtracts %s'), pdf=dict(argstr='-pdf %s'), seed_file=dict(argstr='-seedfile %s', extensions=None, position=2), stepsize=dict(argstr='-stepsize %f', requires=['tracker']), tracker=dict(argstr='-tracker %s', usedefault=True), voxel_dims=dict(argstr='-voxeldims %s', units='mm'))
```

## Next Steps


---

*Source: test_auto_TrackPICo.py:6 | Complexity: Beginner | Last updated: 2026-05-18*