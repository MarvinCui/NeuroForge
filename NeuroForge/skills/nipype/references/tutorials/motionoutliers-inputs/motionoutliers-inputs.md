# How To: Motionoutliers Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test MotionOutliers inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), dummy=dict(argstr='--dummy=%d'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-i %s', extensions=None, mandatory=True), mask=dict(argstr='-m %s', extensions=None), metric=dict(argstr='--%s'), no_motion_correction=dict(argstr='--nomoco'), out_file=dict(argstr='-o %s', extensions=None, hash_files=False, keep_extension=True, name_source='in_file', name_template='%s_outliers.txt'), out_metric_plot=dict(argstr='-p %s', extensions=None, hash_files=False, keep_extension=True, name_source='in_file', name_template='%s_metrics.png'), out_metric_values=dict(argstr='-s %s', extensions=None, hash_files=False, keep_extension=True, name_source='in_file', name_template='%s_metrics.txt'), output_type=dict(), threshold=dict(argstr='--thresh=%g'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), dummy=dict(argstr='--dummy=%d'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-i %s', extensions=None, mandatory=True), mask=dict(argstr='-m %s', extensions=None), metric=dict(argstr='--%s'), no_motion_correction=dict(argstr='--nomoco'), out_file=dict(argstr='-o %s', extensions=None, hash_files=False, keep_extension=True, name_source='in_file', name_template='%s_outliers.txt'), out_metric_plot=dict(argstr='-p %s', extensions=None, hash_files=False, keep_extension=True, name_source='in_file', name_template='%s_metrics.png'), out_metric_values=dict(argstr='-s %s', extensions=None, hash_files=False, keep_extension=True, name_source='in_file', name_template='%s_metrics.txt'), output_type=dict(), threshold=dict(argstr='--thresh=%g'))
```

## Next Steps


---

*Source: test_auto_MotionOutliers.py:6 | Complexity: Beginner | Last updated: 2026-05-18*