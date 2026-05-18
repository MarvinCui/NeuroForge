# How To: Mesd Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test MESD inputs

## Prerequisites

**Required Modules:**
- `odf`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), bgmask=dict(argstr='-bgmask %s', extensions=None), environ=dict(nohash=True, usedefault=True), fastmesd=dict(argstr='-fastmesd', requires=['mepointset']), in_file=dict(argstr='-inputfile %s', extensions=None, mandatory=True, position=1), inputdatatype=dict(argstr='-inputdatatype %s'), inverter=dict(argstr='-filter %s', mandatory=True, position=2), inverter_param=dict(argstr='%f', mandatory=True, position=3, units='NA'), mepointset=dict(argstr='-mepointset %d', units='NA'), out_file=dict(argstr='> %s', extensions=None, genfile=True, position=-1), scheme_file=dict(argstr='-schemefile %s', extensions=None, mandatory=True))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), bgmask=dict(argstr='-bgmask %s', extensions=None), environ=dict(nohash=True, usedefault=True), fastmesd=dict(argstr='-fastmesd', requires=['mepointset']), in_file=dict(argstr='-inputfile %s', extensions=None, mandatory=True, position=1), inputdatatype=dict(argstr='-inputdatatype %s'), inverter=dict(argstr='-filter %s', mandatory=True, position=2), inverter_param=dict(argstr='%f', mandatory=True, position=3, units='NA'), mepointset=dict(argstr='-mepointset %d', units='NA'), out_file=dict(argstr='> %s', extensions=None, genfile=True, position=-1), scheme_file=dict(argstr='-schemefile %s', extensions=None, mandatory=True))
```

## Next Steps


---

*Source: test_auto_MESD.py:6 | Complexity: Beginner | Last updated: 2026-05-18*