# How To: Tcorrelate Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test TCorrelate inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), num_threads=dict(nohash=True, usedefault=True), out_file=dict(argstr='-prefix %s', extensions=None, name_source='xset', name_template='%s_tcorr'), outputtype=dict(), pearson=dict(argstr='-pearson'), polort=dict(argstr='-polort %d'), xset=dict(argstr='%s', copyfile=False, extensions=None, mandatory=True, position=-2), yset=dict(argstr='%s', copyfile=False, extensions=None, mandatory=True, position=-1))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), num_threads=dict(nohash=True, usedefault=True), out_file=dict(argstr='-prefix %s', extensions=None, name_source='xset', name_template='%s_tcorr'), outputtype=dict(), pearson=dict(argstr='-pearson'), polort=dict(argstr='-polort %d'), xset=dict(argstr='%s', copyfile=False, extensions=None, mandatory=True, position=-2), yset=dict(argstr='%s', copyfile=False, extensions=None, mandatory=True, position=-1))
```

## Next Steps


---

*Source: test_auto_TCorrelate.py:6 | Complexity: Beginner | Last updated: 2026-05-18*