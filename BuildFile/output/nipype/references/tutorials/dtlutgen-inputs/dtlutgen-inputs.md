# How To: Dtlutgen Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test DTLUTGen inputs

## Prerequisites

**Required Modules:**
- `dti`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(acg=dict(argstr='-acg'), args=dict(argstr='%s'), bingham=dict(argstr='-bingham'), environ=dict(nohash=True, usedefault=True), frange=dict(argstr='-frange %s', position=1, units='NA'), inversion=dict(argstr='-inversion %d', units='NA'), lrange=dict(argstr='-lrange %s', position=1, units='NA'), out_file=dict(argstr='> %s', extensions=None, genfile=True, position=-1), samples=dict(argstr='-samples %d', units='NA'), scheme_file=dict(argstr='-schemefile %s', extensions=None, mandatory=True, position=2), snr=dict(argstr='-snr %f', units='NA'), step=dict(argstr='-step %f', units='NA'), trace=dict(argstr='-trace %G', units='NA'), watson=dict(argstr='-watson'))
```


## Complete Example

```python
# Workflow
input_map = dict(acg=dict(argstr='-acg'), args=dict(argstr='%s'), bingham=dict(argstr='-bingham'), environ=dict(nohash=True, usedefault=True), frange=dict(argstr='-frange %s', position=1, units='NA'), inversion=dict(argstr='-inversion %d', units='NA'), lrange=dict(argstr='-lrange %s', position=1, units='NA'), out_file=dict(argstr='> %s', extensions=None, genfile=True, position=-1), samples=dict(argstr='-samples %d', units='NA'), scheme_file=dict(argstr='-schemefile %s', extensions=None, mandatory=True, position=2), snr=dict(argstr='-snr %f', units='NA'), step=dict(argstr='-step %f', units='NA'), trace=dict(argstr='-trace %G', units='NA'), watson=dict(argstr='-watson'))
```

## Next Steps


---

*Source: test_auto_DTLUTGen.py:6 | Complexity: Beginner | Last updated: 2026-05-18*