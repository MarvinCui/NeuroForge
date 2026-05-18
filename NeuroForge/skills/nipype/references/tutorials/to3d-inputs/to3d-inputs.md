# How To: To3D Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test To3D inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), assumemosaic=dict(argstr='-assume_dicom_mosaic'), datatype=dict(argstr='-datum %s'), environ=dict(nohash=True, usedefault=True), filetype=dict(argstr='-%s'), funcparams=dict(argstr='-time:zt %s alt+z2'), in_folder=dict(argstr='%s/*.dcm', mandatory=True, position=-1), num_threads=dict(nohash=True, usedefault=True), out_file=dict(argstr='-prefix %s', extensions=None, name_source=['in_folder'], name_template='%s'), outputtype=dict(), skipoutliers=dict(argstr='-skip_outliers'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), assumemosaic=dict(argstr='-assume_dicom_mosaic'), datatype=dict(argstr='-datum %s'), environ=dict(nohash=True, usedefault=True), filetype=dict(argstr='-%s'), funcparams=dict(argstr='-time:zt %s alt+z2'), in_folder=dict(argstr='%s/*.dcm', mandatory=True, position=-1), num_threads=dict(nohash=True, usedefault=True), out_file=dict(argstr='-prefix %s', extensions=None, name_source=['in_folder'], name_template='%s'), outputtype=dict(), skipoutliers=dict(argstr='-skip_outliers'))
```

## Next Steps


---

*Source: test_auto_To3D.py:6 | Complexity: Beginner | Last updated: 2026-05-18*