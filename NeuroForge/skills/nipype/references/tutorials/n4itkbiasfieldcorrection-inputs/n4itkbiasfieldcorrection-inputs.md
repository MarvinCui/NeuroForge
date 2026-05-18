# How To: N4Itkbiasfieldcorrection Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test N4ITKBiasFieldCorrection inputs

## Prerequisites

**Required Modules:**
- `n4itkbiasfieldcorrection`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), bsplineorder=dict(argstr='--bsplineorder %d'), convergencethreshold=dict(argstr='--convergencethreshold %f'), environ=dict(nohash=True, usedefault=True), histogramsharpening=dict(argstr='--histogramsharpening %s', sep=','), inputimage=dict(argstr='--inputimage %s', extensions=None), iterations=dict(argstr='--iterations %s', sep=','), maskimage=dict(argstr='--maskimage %s', extensions=None), meshresolution=dict(argstr='--meshresolution %s', sep=','), outputbiasfield=dict(argstr='--outputbiasfield %s', hash_files=False), outputimage=dict(argstr='--outputimage %s', hash_files=False), shrinkfactor=dict(argstr='--shrinkfactor %d'), splinedistance=dict(argstr='--splinedistance %f'), weightimage=dict(argstr='--weightimage %s', extensions=None))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), bsplineorder=dict(argstr='--bsplineorder %d'), convergencethreshold=dict(argstr='--convergencethreshold %f'), environ=dict(nohash=True, usedefault=True), histogramsharpening=dict(argstr='--histogramsharpening %s', sep=','), inputimage=dict(argstr='--inputimage %s', extensions=None), iterations=dict(argstr='--iterations %s', sep=','), maskimage=dict(argstr='--maskimage %s', extensions=None), meshresolution=dict(argstr='--meshresolution %s', sep=','), outputbiasfield=dict(argstr='--outputbiasfield %s', hash_files=False), outputimage=dict(argstr='--outputimage %s', hash_files=False), shrinkfactor=dict(argstr='--shrinkfactor %d'), splinedistance=dict(argstr='--splinedistance %f'), weightimage=dict(argstr='--weightimage %s', extensions=None))
```

## Next Steps


---

*Source: test_auto_N4ITKBiasFieldCorrection.py:6 | Complexity: Beginner | Last updated: 2026-05-18*