# How To: Hardimat Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test HARDIMat inputs

## Prerequisites

**Required Modules:**
- `odf`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), bvals=dict(extensions=None, mandatory=True), bvecs=dict(argstr='%s', extensions=None, mandatory=True, position=1), environ=dict(nohash=True, usedefault=True), image_info=dict(argstr='-info %s', extensions=None), image_orientation_vectors=dict(argstr='-iop %f'), oblique_correction=dict(argstr='-oc'), odf_file=dict(argstr='-odf %s', extensions=None), order=dict(argstr='-order %s'), out_file=dict(argstr='%s', extensions=None, position=2, usedefault=True), reference_file=dict(argstr='-ref %s', extensions=None))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), bvals=dict(extensions=None, mandatory=True), bvecs=dict(argstr='%s', extensions=None, mandatory=True, position=1), environ=dict(nohash=True, usedefault=True), image_info=dict(argstr='-info %s', extensions=None), image_orientation_vectors=dict(argstr='-iop %f'), oblique_correction=dict(argstr='-oc'), odf_file=dict(argstr='-odf %s', extensions=None), order=dict(argstr='-order %s'), out_file=dict(argstr='%s', extensions=None, position=2, usedefault=True), reference_file=dict(argstr='-ref %s', extensions=None))
```

## Next Steps


---

*Source: test_auto_HARDIMat.py:6 | Complexity: Beginner | Last updated: 2026-05-18*