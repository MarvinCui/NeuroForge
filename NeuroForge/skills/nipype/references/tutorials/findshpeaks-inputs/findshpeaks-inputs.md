# How To: Findshpeaks Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test FindShPeaks inputs

## Prerequisites

**Required Modules:**
- `tensors`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), directions_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), display_debug=dict(argstr='-debug'), display_info=dict(argstr='-info'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-3), num_peaks=dict(argstr='-num %s'), out_file=dict(argstr='%s', extensions=None, hash_files=False, keep_extension=False, name_source=['in_file'], name_template='%s_peak_dirs.mif', position=-1), peak_directions=dict(argstr='-direction %s', sep=' '), peak_threshold=dict(argstr='-threshold %s'), peaks_image=dict(argstr='-peaks %s', extensions=None), quiet_display=dict(argstr='-quiet'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), directions_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), display_debug=dict(argstr='-debug'), display_info=dict(argstr='-info'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-3), num_peaks=dict(argstr='-num %s'), out_file=dict(argstr='%s', extensions=None, hash_files=False, keep_extension=False, name_source=['in_file'], name_template='%s_peak_dirs.mif', position=-1), peak_directions=dict(argstr='-direction %s', sep=' '), peak_threshold=dict(argstr='-threshold %s'), peaks_image=dict(argstr='-peaks %s', extensions=None), quiet_display=dict(argstr='-quiet'))
```

## Next Steps


---

*Source: test_auto_FindShPeaks.py:6 | Complexity: Beginner | Last updated: 2026-05-18*