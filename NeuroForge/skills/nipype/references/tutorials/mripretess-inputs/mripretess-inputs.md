# How To: Mripretess Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test MRIPretess inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_filled=dict(argstr='%s', extensions=None, mandatory=True, position=-4), in_norm=dict(argstr='%s', extensions=None, mandatory=True, position=-2), keep=dict(argstr='-keep'), label=dict(argstr='%s', mandatory=True, position=-3, usedefault=True), nocorners=dict(argstr='-nocorners'), out_file=dict(argstr='%s', extensions=None, keep_extension=True, name_source=['in_filled'], name_template='%s_pretesswm', position=-1), subjects_dir=dict(), test=dict(argstr='-test'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_filled=dict(argstr='%s', extensions=None, mandatory=True, position=-4), in_norm=dict(argstr='%s', extensions=None, mandatory=True, position=-2), keep=dict(argstr='-keep'), label=dict(argstr='%s', mandatory=True, position=-3, usedefault=True), nocorners=dict(argstr='-nocorners'), out_file=dict(argstr='%s', extensions=None, keep_extension=True, name_source=['in_filled'], name_template='%s_pretesswm', position=-1), subjects_dir=dict(), test=dict(argstr='-test'))
```

## Next Steps


---

*Source: test_auto_MRIPretess.py:6 | Complexity: Beginner | Last updated: 2026-05-18*