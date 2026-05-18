# How To: Metricresample Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test MetricResample inputs

## Prerequisites

**Required Modules:**
- `metric`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(area_metrics=dict(argstr='-area-metrics', position=5, xor=['area_surfs']), area_surfs=dict(argstr='-area-surfs', position=5, xor=['area_metrics']), args=dict(argstr='%s'), current_area=dict(argstr='%s', extensions=None, position=6), current_sphere=dict(argstr='%s', extensions=None, mandatory=True, position=1), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=0), largest=dict(argstr='-largest', position=10), method=dict(argstr='%s', mandatory=True, position=3), new_area=dict(argstr='%s', extensions=None, position=7), new_sphere=dict(argstr='%s', extensions=None, mandatory=True, position=2), out_file=dict(argstr='%s', extensions=None, keep_extension=True, name_source=['new_sphere'], name_template='%s.out', position=4), roi_metric=dict(argstr='-current-roi %s', extensions=None, position=8), valid_roi_out=dict(argstr='-valid-roi-out', position=9))
```


## Complete Example

```python
# Workflow
input_map = dict(area_metrics=dict(argstr='-area-metrics', position=5, xor=['area_surfs']), area_surfs=dict(argstr='-area-surfs', position=5, xor=['area_metrics']), args=dict(argstr='%s'), current_area=dict(argstr='%s', extensions=None, position=6), current_sphere=dict(argstr='%s', extensions=None, mandatory=True, position=1), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=0), largest=dict(argstr='-largest', position=10), method=dict(argstr='%s', mandatory=True, position=3), new_area=dict(argstr='%s', extensions=None, position=7), new_sphere=dict(argstr='%s', extensions=None, mandatory=True, position=2), out_file=dict(argstr='%s', extensions=None, keep_extension=True, name_source=['new_sphere'], name_template='%s.out', position=4), roi_metric=dict(argstr='-current-roi %s', extensions=None, position=8), valid_roi_out=dict(argstr='-valid-roi-out', position=9))
```

## Next Steps


---

*Source: test_auto_MetricResample.py:6 | Complexity: Beginner | Last updated: 2026-05-18*