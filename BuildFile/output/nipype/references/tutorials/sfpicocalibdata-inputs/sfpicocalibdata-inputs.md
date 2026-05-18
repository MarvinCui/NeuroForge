# How To: Sfpicocalibdata Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test SFPICOCalibData inputs

## Prerequisites

**Required Modules:**
- `calib`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), info_file=dict(argstr='-infooutputfile %s', extensions=None, genfile=True, hash_files=False, mandatory=True), onedtfarange=dict(argstr='-onedtfarange %s', units='NA'), onedtfastep=dict(argstr='-onedtfastep %f', units='NA'), out_file=dict(argstr='> %s', extensions=None, genfile=True, position=-1), scheme_file=dict(argstr='-schemefile %s', extensions=None, mandatory=True), seed=dict(argstr='-seed %f', units='NA'), snr=dict(argstr='-snr %f', units='NA'), trace=dict(argstr='-trace %f', units='NA'), twodtanglerange=dict(argstr='-twodtanglerange %s', units='NA'), twodtanglestep=dict(argstr='-twodtanglestep %f', units='NA'), twodtfarange=dict(argstr='-twodtfarange %s', units='NA'), twodtfastep=dict(argstr='-twodtfastep %f', units='NA'), twodtmixmax=dict(argstr='-twodtmixmax %f', units='NA'), twodtmixstep=dict(argstr='-twodtmixstep %f', units='NA'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), info_file=dict(argstr='-infooutputfile %s', extensions=None, genfile=True, hash_files=False, mandatory=True), onedtfarange=dict(argstr='-onedtfarange %s', units='NA'), onedtfastep=dict(argstr='-onedtfastep %f', units='NA'), out_file=dict(argstr='> %s', extensions=None, genfile=True, position=-1), scheme_file=dict(argstr='-schemefile %s', extensions=None, mandatory=True), seed=dict(argstr='-seed %f', units='NA'), snr=dict(argstr='-snr %f', units='NA'), trace=dict(argstr='-trace %f', units='NA'), twodtanglerange=dict(argstr='-twodtanglerange %s', units='NA'), twodtanglestep=dict(argstr='-twodtanglestep %f', units='NA'), twodtfarange=dict(argstr='-twodtfarange %s', units='NA'), twodtfastep=dict(argstr='-twodtfastep %f', units='NA'), twodtmixmax=dict(argstr='-twodtmixmax %f', units='NA'), twodtmixstep=dict(argstr='-twodtmixstep %f', units='NA'))
```

## Next Steps


---

*Source: test_auto_SFPICOCalibData.py:6 | Complexity: Beginner | Last updated: 2026-05-18*