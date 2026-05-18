# How To: Nlpfit Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test NlpFit inputs

## Prerequisites

**Required Modules:**
- `minc`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), clobber=dict(argstr='-clobber', usedefault=True), config_file=dict(argstr='-config_file %s', extensions=None, mandatory=True), environ=dict(nohash=True, usedefault=True), init_xfm=dict(argstr='-init_xfm %s', extensions=None, mandatory=True), input_grid_files=dict(), output_xfm=dict(argstr='%s', extensions=None, genfile=True, position=-1), source=dict(argstr='%s', extensions=None, mandatory=True, position=-3), source_mask=dict(argstr='-source_mask %s', extensions=None, mandatory=True), target=dict(argstr='%s', extensions=None, mandatory=True, position=-2), verbose=dict(argstr='-verbose'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), clobber=dict(argstr='-clobber', usedefault=True), config_file=dict(argstr='-config_file %s', extensions=None, mandatory=True), environ=dict(nohash=True, usedefault=True), init_xfm=dict(argstr='-init_xfm %s', extensions=None, mandatory=True), input_grid_files=dict(), output_xfm=dict(argstr='%s', extensions=None, genfile=True, position=-1), source=dict(argstr='%s', extensions=None, mandatory=True, position=-3), source_mask=dict(argstr='-source_mask %s', extensions=None, mandatory=True), target=dict(argstr='%s', extensions=None, mandatory=True, position=-2), verbose=dict(argstr='-verbose'))
```

## Next Steps


---

*Source: test_auto_NlpFit.py:6 | Complexity: Beginner | Last updated: 2026-05-18*