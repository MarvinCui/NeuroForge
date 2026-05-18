# How To: Blurinmask Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test BlurInMask inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), automask=dict(argstr='-automask'), environ=dict(nohash=True, usedefault=True), float_out=dict(argstr='-float'), fwhm=dict(argstr='-FWHM %f', mandatory=True), in_file=dict(argstr='-input %s', copyfile=False, extensions=None, mandatory=True, position=1), mask=dict(argstr='-mask %s', extensions=None), multimask=dict(argstr='-Mmask %s', extensions=None), num_threads=dict(nohash=True, usedefault=True), options=dict(argstr='%s', position=2), out_file=dict(argstr='-prefix %s', extensions=None, name_source='in_file', name_template='%s_blur', position=-1), outputtype=dict(), preserve=dict(argstr='-preserve'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), automask=dict(argstr='-automask'), environ=dict(nohash=True, usedefault=True), float_out=dict(argstr='-float'), fwhm=dict(argstr='-FWHM %f', mandatory=True), in_file=dict(argstr='-input %s', copyfile=False, extensions=None, mandatory=True, position=1), mask=dict(argstr='-mask %s', extensions=None), multimask=dict(argstr='-Mmask %s', extensions=None), num_threads=dict(nohash=True, usedefault=True), options=dict(argstr='%s', position=2), out_file=dict(argstr='-prefix %s', extensions=None, name_source='in_file', name_template='%s_blur', position=-1), outputtype=dict(), preserve=dict(argstr='-preserve'))
```

## Next Steps


---

*Source: test_auto_BlurInMask.py:6 | Complexity: Beginner | Last updated: 2026-05-18*