# How To: Ciftismooth Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test CiftiSmooth inputs

## Prerequisites

**Required Modules:**
- `cifti`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), cerebellum_corrected_areas=dict(argstr='cerebellum-corrected-areas %s', extensions=None, position=10, requires=['cerebellum_surf']), cerebellum_surf=dict(argstr='-cerebellum-surface %s', extensions=None, position=9), cifti_roi=dict(argstr='-cifti-roi %s', extensions=None, position=11), direction=dict(argstr='%s', mandatory=True, position=3), environ=dict(nohash=True, usedefault=True), fix_zeros_surf=dict(argstr='-fix-zeros-surface', position=13), fix_zeros_vol=dict(argstr='-fix-zeros-volume', position=12), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=0), left_corrected_areas=dict(argstr='-left-corrected-areas %s', extensions=None, position=6), left_surf=dict(argstr='-left-surface %s', extensions=None, mandatory=True, position=5), merged_volume=dict(argstr='-merged-volume', position=14), out_file=dict(argstr='%s', extensions=None, keep_extension=True, name_source=['in_file'], name_template='smoothed_%s.nii', position=4), right_corrected_areas=dict(argstr='-right-corrected-areas %s', extensions=None, position=8), right_surf=dict(argstr='-right-surface %s', extensions=None, mandatory=True, position=7), sigma_surf=dict(argstr='%s', mandatory=True, position=1), sigma_vol=dict(argstr='%s', mandatory=True, position=2))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), cerebellum_corrected_areas=dict(argstr='cerebellum-corrected-areas %s', extensions=None, position=10, requires=['cerebellum_surf']), cerebellum_surf=dict(argstr='-cerebellum-surface %s', extensions=None, position=9), cifti_roi=dict(argstr='-cifti-roi %s', extensions=None, position=11), direction=dict(argstr='%s', mandatory=True, position=3), environ=dict(nohash=True, usedefault=True), fix_zeros_surf=dict(argstr='-fix-zeros-surface', position=13), fix_zeros_vol=dict(argstr='-fix-zeros-volume', position=12), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=0), left_corrected_areas=dict(argstr='-left-corrected-areas %s', extensions=None, position=6), left_surf=dict(argstr='-left-surface %s', extensions=None, mandatory=True, position=5), merged_volume=dict(argstr='-merged-volume', position=14), out_file=dict(argstr='%s', extensions=None, keep_extension=True, name_source=['in_file'], name_template='smoothed_%s.nii', position=4), right_corrected_areas=dict(argstr='-right-corrected-areas %s', extensions=None, position=8), right_surf=dict(argstr='-right-surface %s', extensions=None, mandatory=True, position=7), sigma_surf=dict(argstr='%s', mandatory=True, position=1), sigma_vol=dict(argstr='%s', mandatory=True, position=2))
```

## Next Steps


---

*Source: test_auto_CiftiSmooth.py:6 | Complexity: Beginner | Last updated: 2026-05-18*