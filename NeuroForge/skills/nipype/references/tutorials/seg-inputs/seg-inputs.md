# How To: Seg Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Seg inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), bias_classes=dict(argstr='-bias_classes %s'), bias_fwhm=dict(argstr='-bias_fwhm %f'), blur_meth=dict(argstr='-blur_meth %s'), bmrf=dict(argstr='-bmrf %f'), classes=dict(argstr='-classes %s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-anat %s', copyfile=True, extensions=None, mandatory=True, position=-1), main_N=dict(argstr='-main_N %d'), mask=dict(argstr='-mask %s', mandatory=True, position=-2), mixfloor=dict(argstr='-mixfloor %f'), mixfrac=dict(argstr='-mixfrac %s'), prefix=dict(argstr='-prefix %s'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), bias_classes=dict(argstr='-bias_classes %s'), bias_fwhm=dict(argstr='-bias_fwhm %f'), blur_meth=dict(argstr='-blur_meth %s'), bmrf=dict(argstr='-bmrf %f'), classes=dict(argstr='-classes %s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-anat %s', copyfile=True, extensions=None, mandatory=True, position=-1), main_N=dict(argstr='-main_N %d'), mask=dict(argstr='-mask %s', mandatory=True, position=-2), mixfloor=dict(argstr='-mixfloor %f'), mixfrac=dict(argstr='-mixfrac %s'), prefix=dict(argstr='-prefix %s'))
```

## Next Steps


---

*Source: test_auto_Seg.py:6 | Complexity: Beginner | Last updated: 2026-05-18*