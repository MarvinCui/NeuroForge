# How To: Hist Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Hist inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), bin_width=dict(argstr='-binwidth %f'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-input %s', copyfile=False, extensions=None, mandatory=True, position=1), mask=dict(argstr='-mask %s', extensions=None), max_value=dict(argstr='-max %f'), min_value=dict(argstr='-min %f'), nbin=dict(argstr='-nbin %d'), out_file=dict(argstr='-prefix %s', extensions=None, keep_extension=False, name_source=['in_file'], name_template='%s_hist'), out_show=dict(argstr='> %s', extensions=None, keep_extension=False, name_source='in_file', name_template='%s_hist.out', position=-1), showhist=dict(argstr='-showhist', usedefault=True))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), bin_width=dict(argstr='-binwidth %f'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-input %s', copyfile=False, extensions=None, mandatory=True, position=1), mask=dict(argstr='-mask %s', extensions=None), max_value=dict(argstr='-max %f'), min_value=dict(argstr='-min %f'), nbin=dict(argstr='-nbin %d'), out_file=dict(argstr='-prefix %s', extensions=None, keep_extension=False, name_source=['in_file'], name_template='%s_hist'), out_show=dict(argstr='> %s', extensions=None, keep_extension=False, name_source='in_file', name_template='%s_hist.out', position=-1), showhist=dict(argstr='-showhist', usedefault=True))
```

## Next Steps


---

*Source: test_auto_Hist.py:6 | Complexity: Beginner | Last updated: 2026-05-18*