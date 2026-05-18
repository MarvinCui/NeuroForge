# How To: Onedtoolpy Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test OneDToolPy inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), censor_motion=dict(argstr='-censor_motion %f %s'), censor_prev_TR=dict(argstr='-censor_prev_TR'), demean=dict(argstr='-demean'), derivative=dict(argstr='-derivative'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-infile %s', extensions=None, mandatory=True), out_file=dict(argstr='-write %s', extensions=None, xor=['show_cormat_warnings']), outputtype=dict(), py27_path=dict(usedefault=True), set_nruns=dict(argstr='-set_nruns %d'), show_censor_count=dict(argstr='-show_censor_count'), show_cormat_warnings=dict(argstr='-show_cormat_warnings |& tee %s', extensions=None, position=-1, xor=['out_file']), show_indices_interest=dict(argstr='-show_indices_interest'), show_trs_run=dict(argstr='-show_trs_run %d'), show_trs_uncensored=dict(argstr='-show_trs_uncensored %s'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), censor_motion=dict(argstr='-censor_motion %f %s'), censor_prev_TR=dict(argstr='-censor_prev_TR'), demean=dict(argstr='-demean'), derivative=dict(argstr='-derivative'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-infile %s', extensions=None, mandatory=True), out_file=dict(argstr='-write %s', extensions=None, xor=['show_cormat_warnings']), outputtype=dict(), py27_path=dict(usedefault=True), set_nruns=dict(argstr='-set_nruns %d'), show_censor_count=dict(argstr='-show_censor_count'), show_cormat_warnings=dict(argstr='-show_cormat_warnings |& tee %s', extensions=None, position=-1, xor=['out_file']), show_indices_interest=dict(argstr='-show_indices_interest'), show_trs_run=dict(argstr='-show_trs_run %d'), show_trs_uncensored=dict(argstr='-show_trs_uncensored %s'))
```

## Next Steps


---

*Source: test_auto_OneDToolPy.py:6 | Complexity: Beginner | Last updated: 2026-05-18*