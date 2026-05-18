# How To: Calabel Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test CALabel inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(align=dict(argstr='-align'), args=dict(argstr='%s'), aseg=dict(argstr='-aseg %s', extensions=None), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-4), in_vol=dict(argstr='-r %s', extensions=None), intensities=dict(argstr='-r %s', extensions=None), label=dict(argstr='-l %s', extensions=None), no_big_ventricles=dict(argstr='-nobigventricles'), num_threads=dict(), out_file=dict(argstr='%s', extensions=None, mandatory=True, position=-1), prior=dict(argstr='-prior %.1f'), relabel_unlikely=dict(argstr='-relabel_unlikely %d %.1f'), subjects_dir=dict(), template=dict(argstr='%s', extensions=None, mandatory=True, position=-2), transform=dict(argstr='%s', extensions=None, mandatory=True, position=-3))
```


## Complete Example

```python
# Workflow
input_map = dict(align=dict(argstr='-align'), args=dict(argstr='%s'), aseg=dict(argstr='-aseg %s', extensions=None), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-4), in_vol=dict(argstr='-r %s', extensions=None), intensities=dict(argstr='-r %s', extensions=None), label=dict(argstr='-l %s', extensions=None), no_big_ventricles=dict(argstr='-nobigventricles'), num_threads=dict(), out_file=dict(argstr='%s', extensions=None, mandatory=True, position=-1), prior=dict(argstr='-prior %.1f'), relabel_unlikely=dict(argstr='-relabel_unlikely %d %.1f'), subjects_dir=dict(), template=dict(argstr='%s', extensions=None, mandatory=True, position=-2), transform=dict(argstr='%s', extensions=None, mandatory=True, position=-3))
```

## Next Steps


---

*Source: test_auto_CALabel.py:6 | Complexity: Beginner | Last updated: 2026-05-18*