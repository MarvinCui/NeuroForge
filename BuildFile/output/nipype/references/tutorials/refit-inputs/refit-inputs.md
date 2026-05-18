# How To: Refit Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Refit inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), atrcopy=dict(argstr='-atrcopy %s %s'), atrfloat=dict(argstr='-atrfloat %s %s'), atrint=dict(argstr='-atrint %s %s'), atrstring=dict(argstr='-atrstring %s %s'), deoblique=dict(argstr='-deoblique'), duporigin_file=dict(argstr='-duporigin %s', extensions=None), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', copyfile=True, extensions=None, mandatory=True, position=-1), nosaveatr=dict(argstr='-nosaveatr'), saveatr=dict(argstr='-saveatr'), space=dict(argstr='-space %s'), xdel=dict(argstr='-xdel %f'), xorigin=dict(argstr='-xorigin %s'), xyzscale=dict(argstr='-xyzscale %f'), ydel=dict(argstr='-ydel %f'), yorigin=dict(argstr='-yorigin %s'), zdel=dict(argstr='-zdel %f'), zorigin=dict(argstr='-zorigin %s'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), atrcopy=dict(argstr='-atrcopy %s %s'), atrfloat=dict(argstr='-atrfloat %s %s'), atrint=dict(argstr='-atrint %s %s'), atrstring=dict(argstr='-atrstring %s %s'), deoblique=dict(argstr='-deoblique'), duporigin_file=dict(argstr='-duporigin %s', extensions=None), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', copyfile=True, extensions=None, mandatory=True, position=-1), nosaveatr=dict(argstr='-nosaveatr'), saveatr=dict(argstr='-saveatr'), space=dict(argstr='-space %s'), xdel=dict(argstr='-xdel %f'), xorigin=dict(argstr='-xorigin %s'), xyzscale=dict(argstr='-xyzscale %f'), ydel=dict(argstr='-ydel %f'), yorigin=dict(argstr='-yorigin %s'), zdel=dict(argstr='-zdel %f'), zorigin=dict(argstr='-zorigin %s'))
```

## Next Steps


---

*Source: test_auto_Refit.py:6 | Complexity: Beginner | Last updated: 2026-05-18*