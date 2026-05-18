# How To: Thresholdimage Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test ThresholdImage inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), copy_header=dict(mandatory=True, usedefault=True), dimension=dict(argstr='%d', position=1, usedefault=True), environ=dict(nohash=True, usedefault=True), input_image=dict(argstr='%s', extensions=None, mandatory=True, position=2), input_mask=dict(argstr='%s', extensions=None, requires=['num_thresholds']), inside_value=dict(argstr='%f', position=6, requires=['th_low']), mode=dict(argstr='%s', position=4, requires=['num_thresholds'], xor=['th_low', 'th_high']), num_threads=dict(nohash=True, usedefault=True), num_thresholds=dict(argstr='%d', position=5), output_image=dict(argstr='%s', extensions=None, keep_extension=True, name_source=['input_image'], name_template='%s_resampled', position=3), outside_value=dict(argstr='%f', position=7, requires=['th_low']), th_high=dict(argstr='%f', position=5, xor=['mode']), th_low=dict(argstr='%f', position=4, xor=['mode']))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), copy_header=dict(mandatory=True, usedefault=True), dimension=dict(argstr='%d', position=1, usedefault=True), environ=dict(nohash=True, usedefault=True), input_image=dict(argstr='%s', extensions=None, mandatory=True, position=2), input_mask=dict(argstr='%s', extensions=None, requires=['num_thresholds']), inside_value=dict(argstr='%f', position=6, requires=['th_low']), mode=dict(argstr='%s', position=4, requires=['num_thresholds'], xor=['th_low', 'th_high']), num_threads=dict(nohash=True, usedefault=True), num_thresholds=dict(argstr='%d', position=5), output_image=dict(argstr='%s', extensions=None, keep_extension=True, name_source=['input_image'], name_template='%s_resampled', position=3), outside_value=dict(argstr='%f', position=7, requires=['th_low']), th_high=dict(argstr='%f', position=5, xor=['mode']), th_low=dict(argstr='%f', position=4, xor=['mode']))
```

## Next Steps


---

*Source: test_auto_ThresholdImage.py:6 | Complexity: Beginner | Last updated: 2026-05-18*