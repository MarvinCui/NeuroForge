# How To: Tnorm Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test TNorm inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(L1fit=dict(argstr='-L1fit'), args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', copyfile=False, extensions=None, mandatory=True, position=-1), norm1=dict(argstr='-norm1'), norm2=dict(argstr='-norm2'), normR=dict(argstr='-normR'), normx=dict(argstr='-normx'), num_threads=dict(nohash=True, usedefault=True), out_file=dict(argstr='-prefix %s', extensions=None, name_source='in_file', name_template='%s_tnorm'), outputtype=dict(), polort=dict(argstr='-polort %s'))
```


## Complete Example

```python
# Workflow
input_map = dict(L1fit=dict(argstr='-L1fit'), args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', copyfile=False, extensions=None, mandatory=True, position=-1), norm1=dict(argstr='-norm1'), norm2=dict(argstr='-norm2'), normR=dict(argstr='-normR'), normx=dict(argstr='-normx'), num_threads=dict(nohash=True, usedefault=True), out_file=dict(argstr='-prefix %s', extensions=None, name_source='in_file', name_template='%s_tnorm'), outputtype=dict(), polort=dict(argstr='-polort %s'))
```

## Next Steps


---

*Source: test_auto_TNorm.py:6 | Complexity: Beginner | Last updated: 2026-05-18*