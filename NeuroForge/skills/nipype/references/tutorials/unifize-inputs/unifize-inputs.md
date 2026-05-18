# How To: Unifize Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Unifize inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), cl_frac=dict(argstr='-clfrac %f'), environ=dict(nohash=True, usedefault=True), epi=dict(argstr='-EPI', requires=['no_duplo', 't2'], xor=['gm']), gm=dict(argstr='-GM'), in_file=dict(argstr='-input %s', copyfile=False, extensions=None, mandatory=True, position=-1), no_duplo=dict(argstr='-noduplo'), num_threads=dict(nohash=True, usedefault=True), out_file=dict(argstr='-prefix %s', extensions=None, name_source='in_file', name_template='%s_unifized'), outputtype=dict(), quiet=dict(argstr='-quiet'), rbt=dict(argstr='-rbt %f %f %f'), scale_file=dict(argstr='-ssave %s', extensions=None), t2=dict(argstr='-T2'), t2_up=dict(argstr='-T2up %f'), urad=dict(argstr='-Urad %s'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), cl_frac=dict(argstr='-clfrac %f'), environ=dict(nohash=True, usedefault=True), epi=dict(argstr='-EPI', requires=['no_duplo', 't2'], xor=['gm']), gm=dict(argstr='-GM'), in_file=dict(argstr='-input %s', copyfile=False, extensions=None, mandatory=True, position=-1), no_duplo=dict(argstr='-noduplo'), num_threads=dict(nohash=True, usedefault=True), out_file=dict(argstr='-prefix %s', extensions=None, name_source='in_file', name_template='%s_unifized'), outputtype=dict(), quiet=dict(argstr='-quiet'), rbt=dict(argstr='-rbt %f %f %f'), scale_file=dict(argstr='-ssave %s', extensions=None), t2=dict(argstr='-T2'), t2_up=dict(argstr='-T2up %f'), urad=dict(argstr='-Urad %s'))
```

## Next Steps


---

*Source: test_auto_Unifize.py:6 | Complexity: Beginner | Last updated: 2026-05-18*