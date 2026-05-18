# How To: Filllesions Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test FillLesions inputs

## Prerequisites

**Required Modules:**
- `lesions`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), bin_mask=dict(argstr='-mask %s', extensions=None), cwf=dict(argstr='-cwf %f'), debug=dict(argstr='-debug'), environ=dict(nohash=True, usedefault=True), in_dilation=dict(argstr='-dil %d'), in_file=dict(argstr='-i %s', extensions=None, mandatory=True, position=1), lesion_mask=dict(argstr='-l %s', extensions=None, mandatory=True, position=2), match=dict(argstr='-match %f'), other=dict(argstr='-other'), out_datatype=dict(argstr='-odt %s'), out_file=dict(argstr='-o %s', extensions=None, name_source=['in_file'], name_template='%s_lesions_filled.nii.gz', position=3), search=dict(argstr='-search %f'), size=dict(argstr='-size %d'), smooth=dict(argstr='-smo %f'), use_2d=dict(argstr='-2D'), verbose=dict(argstr='-v'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), bin_mask=dict(argstr='-mask %s', extensions=None), cwf=dict(argstr='-cwf %f'), debug=dict(argstr='-debug'), environ=dict(nohash=True, usedefault=True), in_dilation=dict(argstr='-dil %d'), in_file=dict(argstr='-i %s', extensions=None, mandatory=True, position=1), lesion_mask=dict(argstr='-l %s', extensions=None, mandatory=True, position=2), match=dict(argstr='-match %f'), other=dict(argstr='-other'), out_datatype=dict(argstr='-odt %s'), out_file=dict(argstr='-o %s', extensions=None, name_source=['in_file'], name_template='%s_lesions_filled.nii.gz', position=3), search=dict(argstr='-search %f'), size=dict(argstr='-size %d'), smooth=dict(argstr='-smo %f'), use_2d=dict(argstr='-2D'), verbose=dict(argstr='-v'))
```

## Next Steps


---

*Source: test_auto_FillLesions.py:6 | Complexity: Beginner | Last updated: 2026-05-18*