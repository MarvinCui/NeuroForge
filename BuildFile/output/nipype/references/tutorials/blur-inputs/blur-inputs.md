# How To: Blur Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Blur inputs

## Prerequisites

**Required Modules:**
- `minc`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), clobber=dict(argstr='-clobber', usedefault=True), dimensions=dict(argstr='-dimensions %s'), environ=dict(nohash=True, usedefault=True), fwhm=dict(argstr='-fwhm %s', mandatory=True, xor=('fwhm', 'fwhm3d', 'standard_dev')), fwhm3d=dict(argstr='-3dfwhm %s %s %s', mandatory=True, xor=('fwhm', 'fwhm3d', 'standard_dev')), gaussian=dict(argstr='-gaussian', xor=('gaussian', 'rect')), gradient=dict(argstr='-gradient'), input_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), no_apodize=dict(argstr='-no_apodize'), output_file_base=dict(argstr='%s', extensions=None, position=-1), partial=dict(argstr='-partial'), rect=dict(argstr='-rect', xor=('gaussian', 'rect')), standard_dev=dict(argstr='-standarddev %s', mandatory=True, xor=('fwhm', 'fwhm3d', 'standard_dev')))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), clobber=dict(argstr='-clobber', usedefault=True), dimensions=dict(argstr='-dimensions %s'), environ=dict(nohash=True, usedefault=True), fwhm=dict(argstr='-fwhm %s', mandatory=True, xor=('fwhm', 'fwhm3d', 'standard_dev')), fwhm3d=dict(argstr='-3dfwhm %s %s %s', mandatory=True, xor=('fwhm', 'fwhm3d', 'standard_dev')), gaussian=dict(argstr='-gaussian', xor=('gaussian', 'rect')), gradient=dict(argstr='-gradient'), input_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), no_apodize=dict(argstr='-no_apodize'), output_file_base=dict(argstr='%s', extensions=None, position=-1), partial=dict(argstr='-partial'), rect=dict(argstr='-rect', xor=('gaussian', 'rect')), standard_dev=dict(argstr='-standarddev %s', mandatory=True, xor=('fwhm', 'fwhm3d', 'standard_dev')))
```

## Next Steps


---

*Source: test_auto_Blur.py:6 | Complexity: Beginner | Last updated: 2026-05-18*