# How To: Dtirecon Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test DTIRecon inputs

## Prerequisites

**Required Modules:**
- `dti`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(DWI=dict(argstr='%s', extensions=None, mandatory=True, position=1), args=dict(argstr='%s'), b0_threshold=dict(argstr='-b0_th'), bvals=dict(extensions=None, mandatory=True), bvecs=dict(argstr='-gm %s', extensions=None, mandatory=True), environ=dict(nohash=True, usedefault=True), image_orientation_vectors=dict(argstr='-iop %f'), n_averages=dict(argstr='-nex %s'), oblique_correction=dict(argstr='-oc'), out_prefix=dict(argstr='%s', position=2, usedefault=True), output_type=dict(argstr='-ot %s', usedefault=True))
```


## Complete Example

```python
# Workflow
input_map = dict(DWI=dict(argstr='%s', extensions=None, mandatory=True, position=1), args=dict(argstr='%s'), b0_threshold=dict(argstr='-b0_th'), bvals=dict(extensions=None, mandatory=True), bvecs=dict(argstr='-gm %s', extensions=None, mandatory=True), environ=dict(nohash=True, usedefault=True), image_orientation_vectors=dict(argstr='-iop %f'), n_averages=dict(argstr='-nex %s'), oblique_correction=dict(argstr='-oc'), out_prefix=dict(argstr='%s', position=2, usedefault=True), output_type=dict(argstr='-ot %s', usedefault=True))
```

## Next Steps


---

*Source: test_auto_DTIRecon.py:6 | Complexity: Beginner | Last updated: 2026-05-18*