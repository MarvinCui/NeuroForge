# How To: Plottimeseries Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test PlotTimeSeries inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', mandatory=True, position=1), labels=dict(argstr='%s'), legend_file=dict(argstr='--legend=%s', extensions=None), out_file=dict(argstr='-o %s', extensions=None, genfile=True, hash_files=False), output_type=dict(), plot_finish=dict(argstr='--finish=%d', xor=('plot_range',)), plot_range=dict(argstr='%s', xor=('plot_start', 'plot_finish')), plot_size=dict(argstr='%s'), plot_start=dict(argstr='--start=%d', xor=('plot_range',)), sci_notation=dict(argstr='--sci'), title=dict(argstr='%s'), x_precision=dict(argstr='--precision=%d'), x_units=dict(argstr='-u %d', usedefault=True), y_max=dict(argstr='--ymax=%.2f', xor=('y_range',)), y_min=dict(argstr='--ymin=%.2f', xor=('y_range',)), y_range=dict(argstr='%s', xor=('y_min', 'y_max')))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', mandatory=True, position=1), labels=dict(argstr='%s'), legend_file=dict(argstr='--legend=%s', extensions=None), out_file=dict(argstr='-o %s', extensions=None, genfile=True, hash_files=False), output_type=dict(), plot_finish=dict(argstr='--finish=%d', xor=('plot_range',)), plot_range=dict(argstr='%s', xor=('plot_start', 'plot_finish')), plot_size=dict(argstr='%s'), plot_start=dict(argstr='--start=%d', xor=('plot_range',)), sci_notation=dict(argstr='--sci'), title=dict(argstr='%s'), x_precision=dict(argstr='--precision=%d'), x_units=dict(argstr='-u %d', usedefault=True), y_max=dict(argstr='--ymax=%.2f', xor=('y_range',)), y_min=dict(argstr='--ymin=%.2f', xor=('y_range',)), y_range=dict(argstr='%s', xor=('y_min', 'y_max')))
```

## Next Steps


---

*Source: test_auto_PlotTimeSeries.py:6 | Complexity: Beginner | Last updated: 2026-05-18*