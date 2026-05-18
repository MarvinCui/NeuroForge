# How To: Ecm Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test ECM inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), autoclip=dict(argstr='-autoclip'), automask=dict(argstr='-automask'), environ=dict(nohash=True, usedefault=True), eps=dict(argstr='-eps %f'), fecm=dict(argstr='-fecm'), full=dict(argstr='-full'), in_file=dict(argstr='%s', copyfile=False, extensions=None, mandatory=True, position=-1), mask=dict(argstr='-mask %s', extensions=None), max_iter=dict(argstr='-max_iter %d'), memory=dict(argstr='-memory %f'), num_threads=dict(nohash=True, usedefault=True), out_file=dict(argstr='-prefix %s', extensions=None, name_source=['in_file'], name_template='%s_afni'), outputtype=dict(), polort=dict(argstr='-polort %d'), scale=dict(argstr='-scale %f'), shift=dict(argstr='-shift %f'), sparsity=dict(argstr='-sparsity %f'), thresh=dict(argstr='-thresh %f'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), autoclip=dict(argstr='-autoclip'), automask=dict(argstr='-automask'), environ=dict(nohash=True, usedefault=True), eps=dict(argstr='-eps %f'), fecm=dict(argstr='-fecm'), full=dict(argstr='-full'), in_file=dict(argstr='%s', copyfile=False, extensions=None, mandatory=True, position=-1), mask=dict(argstr='-mask %s', extensions=None), max_iter=dict(argstr='-max_iter %d'), memory=dict(argstr='-memory %f'), num_threads=dict(nohash=True, usedefault=True), out_file=dict(argstr='-prefix %s', extensions=None, name_source=['in_file'], name_template='%s_afni'), outputtype=dict(), polort=dict(argstr='-polort %d'), scale=dict(argstr='-scale %f'), shift=dict(argstr='-shift %f'), sparsity=dict(argstr='-sparsity %f'), thresh=dict(argstr='-thresh %f'))
```

## Next Steps


---

*Source: test_auto_ECM.py:6 | Complexity: Beginner | Last updated: 2026-05-18*