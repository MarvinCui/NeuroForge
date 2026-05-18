# How To: Means Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Means inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), count=dict(argstr='-count'), datum=dict(argstr='-datum %s'), environ=dict(nohash=True, usedefault=True), in_file_a=dict(argstr='%s', extensions=None, mandatory=True, position=-2), in_file_b=dict(argstr='%s', extensions=None, position=-1), mask_inter=dict(argstr='-mask_inter'), mask_union=dict(argstr='-mask_union'), non_zero=dict(argstr='-non_zero'), num_threads=dict(nohash=True, usedefault=True), out_file=dict(argstr='-prefix %s', extensions=None, name_source='in_file_a', name_template='%s_mean'), outputtype=dict(), scale=dict(argstr='-%sscale'), sqr=dict(argstr='-sqr'), std_dev=dict(argstr='-stdev'), summ=dict(argstr='-sum'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), count=dict(argstr='-count'), datum=dict(argstr='-datum %s'), environ=dict(nohash=True, usedefault=True), in_file_a=dict(argstr='%s', extensions=None, mandatory=True, position=-2), in_file_b=dict(argstr='%s', extensions=None, position=-1), mask_inter=dict(argstr='-mask_inter'), mask_union=dict(argstr='-mask_union'), non_zero=dict(argstr='-non_zero'), num_threads=dict(nohash=True, usedefault=True), out_file=dict(argstr='-prefix %s', extensions=None, name_source='in_file_a', name_template='%s_mean'), outputtype=dict(), scale=dict(argstr='-%sscale'), sqr=dict(argstr='-sqr'), std_dev=dict(argstr='-stdev'), summ=dict(argstr='-sum'))
```

## Next Steps


---

*Source: test_auto_Means.py:6 | Complexity: Beginner | Last updated: 2026-05-18*