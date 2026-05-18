# How To: Bestlinreg Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test BestLinReg inputs

## Prerequisites

**Required Modules:**
- `minc`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), clobber=dict(argstr='-clobber', usedefault=True), environ=dict(nohash=True, usedefault=True), output_mnc=dict(argstr='%s', extensions=None, genfile=True, hash_files=False, keep_extension=False, name_source=['source'], name_template='%s_bestlinreg.mnc', position=-1), output_xfm=dict(argstr='%s', extensions=None, genfile=True, hash_files=False, keep_extension=False, name_source=['source'], name_template='%s_bestlinreg.xfm', position=-2), source=dict(argstr='%s', extensions=None, mandatory=True, position=-4), target=dict(argstr='%s', extensions=None, mandatory=True, position=-3), verbose=dict(argstr='-verbose'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), clobber=dict(argstr='-clobber', usedefault=True), environ=dict(nohash=True, usedefault=True), output_mnc=dict(argstr='%s', extensions=None, genfile=True, hash_files=False, keep_extension=False, name_source=['source'], name_template='%s_bestlinreg.mnc', position=-1), output_xfm=dict(argstr='%s', extensions=None, genfile=True, hash_files=False, keep_extension=False, name_source=['source'], name_template='%s_bestlinreg.xfm', position=-2), source=dict(argstr='%s', extensions=None, mandatory=True, position=-4), target=dict(argstr='%s', extensions=None, mandatory=True, position=-3), verbose=dict(argstr='-verbose'))
```

## Next Steps


---

*Source: test_auto_BestLinReg.py:6 | Complexity: Beginner | Last updated: 2026-05-18*