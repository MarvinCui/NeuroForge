# How To: Fwhmx Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test FWHMx inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(acf=dict(argstr='-acf', usedefault=True), args=dict(argstr='%s'), arith=dict(argstr='-arith', xor=['geom']), automask=dict(argstr='-automask', usedefault=True), combine=dict(argstr='-combine'), compat=dict(argstr='-compat'), demed=dict(argstr='-demed', xor=['detrend']), detrend=dict(argstr='-detrend', usedefault=True, xor=['demed']), environ=dict(nohash=True, usedefault=True), geom=dict(argstr='-geom', xor=['arith']), in_file=dict(argstr='-input %s', extensions=None, mandatory=True), mask=dict(argstr='-mask %s', extensions=None), out_detrend=dict(argstr='-detprefix %s', extensions=None, keep_extension=False, name_source='in_file', name_template='%s_detrend'), out_file=dict(argstr='> %s', extensions=None, keep_extension=False, name_source='in_file', name_template='%s_fwhmx.out', position=-1), out_subbricks=dict(argstr='-out %s', extensions=None, keep_extension=False, name_source='in_file', name_template='%s_subbricks.out'), unif=dict(argstr='-unif'))
```


## Complete Example

```python
# Workflow
input_map = dict(acf=dict(argstr='-acf', usedefault=True), args=dict(argstr='%s'), arith=dict(argstr='-arith', xor=['geom']), automask=dict(argstr='-automask', usedefault=True), combine=dict(argstr='-combine'), compat=dict(argstr='-compat'), demed=dict(argstr='-demed', xor=['detrend']), detrend=dict(argstr='-detrend', usedefault=True, xor=['demed']), environ=dict(nohash=True, usedefault=True), geom=dict(argstr='-geom', xor=['arith']), in_file=dict(argstr='-input %s', extensions=None, mandatory=True), mask=dict(argstr='-mask %s', extensions=None), out_detrend=dict(argstr='-detprefix %s', extensions=None, keep_extension=False, name_source='in_file', name_template='%s_detrend'), out_file=dict(argstr='> %s', extensions=None, keep_extension=False, name_source='in_file', name_template='%s_fwhmx.out', position=-1), out_subbricks=dict(argstr='-out %s', extensions=None, keep_extension=False, name_source='in_file', name_template='%s_subbricks.out'), unif=dict(argstr='-unif'))
```

## Next Steps


---

*Source: test_auto_FWHMx.py:6 | Complexity: Beginner | Last updated: 2026-05-18*