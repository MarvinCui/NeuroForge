# How To: Dwi2Sphericalharmonicsimage Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test DWI2SphericalHarmonicsImage inputs

## Prerequisites

**Required Modules:**
- `tensors`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), encoding_file=dict(argstr='-grad %s', extensions=None, mandatory=True, position=1), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), maximum_harmonic_order=dict(argstr='-lmax %s'), normalise=dict(argstr='-normalise', position=3), out_filename=dict(argstr='%s', extensions=None, genfile=True, position=-1))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), encoding_file=dict(argstr='-grad %s', extensions=None, mandatory=True, position=1), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), maximum_harmonic_order=dict(argstr='-lmax %s'), normalise=dict(argstr='-normalise', position=3), out_filename=dict(argstr='%s', extensions=None, genfile=True, position=-1))
```

## Next Steps


---

*Source: test_auto_DWI2SphericalHarmonicsImage.py:6 | Complexity: Beginner | Last updated: 2026-05-18*