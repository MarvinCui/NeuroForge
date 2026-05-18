# How To: Overlay Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Overlay inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), auto_thresh_bg=dict(argstr='-a', mandatory=True, position=5, xor=('auto_thresh_bg', 'full_bg_range', 'bg_thresh')), background_image=dict(argstr='%s', extensions=None, mandatory=True, position=4), bg_thresh=dict(argstr='%.3f %.3f', mandatory=True, position=5, xor=('auto_thresh_bg', 'full_bg_range', 'bg_thresh')), environ=dict(nohash=True, usedefault=True), full_bg_range=dict(argstr='-A', mandatory=True, position=5, xor=('auto_thresh_bg', 'full_bg_range', 'bg_thresh')), out_file=dict(argstr='%s', extensions=None, genfile=True, hash_files=False, position=-1), out_type=dict(argstr='%s', position=2, usedefault=True), output_type=dict(), show_negative_stats=dict(argstr='%s', position=8, xor=['stat_image2']), stat_image=dict(argstr='%s', extensions=None, mandatory=True, position=6), stat_image2=dict(argstr='%s', extensions=None, position=9, xor=['show_negative_stats']), stat_thresh=dict(argstr='%.2f %.2f', mandatory=True, position=7), stat_thresh2=dict(argstr='%.2f %.2f', position=10), transparency=dict(argstr='%s', position=1, usedefault=True), use_checkerboard=dict(argstr='-c', position=3))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), auto_thresh_bg=dict(argstr='-a', mandatory=True, position=5, xor=('auto_thresh_bg', 'full_bg_range', 'bg_thresh')), background_image=dict(argstr='%s', extensions=None, mandatory=True, position=4), bg_thresh=dict(argstr='%.3f %.3f', mandatory=True, position=5, xor=('auto_thresh_bg', 'full_bg_range', 'bg_thresh')), environ=dict(nohash=True, usedefault=True), full_bg_range=dict(argstr='-A', mandatory=True, position=5, xor=('auto_thresh_bg', 'full_bg_range', 'bg_thresh')), out_file=dict(argstr='%s', extensions=None, genfile=True, hash_files=False, position=-1), out_type=dict(argstr='%s', position=2, usedefault=True), output_type=dict(), show_negative_stats=dict(argstr='%s', position=8, xor=['stat_image2']), stat_image=dict(argstr='%s', extensions=None, mandatory=True, position=6), stat_image2=dict(argstr='%s', extensions=None, position=9, xor=['show_negative_stats']), stat_thresh=dict(argstr='%.2f %.2f', mandatory=True, position=7), stat_thresh2=dict(argstr='%.2f %.2f', position=10), transparency=dict(argstr='%s', position=1, usedefault=True), use_checkerboard=dict(argstr='-c', position=3))
```

## Next Steps


---

*Source: test_auto_Overlay.py:6 | Complexity: Beginner | Last updated: 2026-05-18*