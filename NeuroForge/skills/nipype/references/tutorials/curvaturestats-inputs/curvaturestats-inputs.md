# How To: Curvaturestats Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test CurvatureStats inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), copy_inputs=dict(), curvfile1=dict(argstr='%s', extensions=None, mandatory=True, position=-2), curvfile2=dict(argstr='%s', extensions=None, mandatory=True, position=-1), environ=dict(nohash=True, usedefault=True), hemisphere=dict(argstr='%s', mandatory=True, position=-3), min_max=dict(argstr='-m'), out_file=dict(argstr='-o %s', extensions=None, hash_files=False, name_source=['hemisphere'], name_template='%s.curv.stats'), subject_id=dict(argstr='%s', mandatory=True, position=-4, usedefault=True), subjects_dir=dict(), surface=dict(argstr='-F %s', extensions=None), values=dict(argstr='-G'), write=dict(argstr='--writeCurvatureFiles'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), copy_inputs=dict(), curvfile1=dict(argstr='%s', extensions=None, mandatory=True, position=-2), curvfile2=dict(argstr='%s', extensions=None, mandatory=True, position=-1), environ=dict(nohash=True, usedefault=True), hemisphere=dict(argstr='%s', mandatory=True, position=-3), min_max=dict(argstr='-m'), out_file=dict(argstr='-o %s', extensions=None, hash_files=False, name_source=['hemisphere'], name_template='%s.curv.stats'), subject_id=dict(argstr='%s', mandatory=True, position=-4, usedefault=True), subjects_dir=dict(), surface=dict(argstr='-F %s', extensions=None), values=dict(argstr='-G'), write=dict(argstr='--writeCurvatureFiles'))
```

## Next Steps


---

*Source: test_auto_CurvatureStats.py:6 | Complexity: Beginner | Last updated: 2026-05-18*