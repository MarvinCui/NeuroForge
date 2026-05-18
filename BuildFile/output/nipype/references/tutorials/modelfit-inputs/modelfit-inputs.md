# How To: Modelfit Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test ModelFit inputs

## Prerequisites

**Required Modules:**
- `dti`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), bgmask=dict(argstr='-bgmask %s', extensions=None), bgthresh=dict(argstr='-bgthresh %G'), cfthresh=dict(argstr='-csfthresh %G'), environ=dict(nohash=True, usedefault=True), fixedbvalue=dict(argstr='-fixedbvalue %s'), fixedmodq=dict(argstr='-fixedmod %s'), in_file=dict(argstr='-inputfile %s', extensions=None, mandatory=True), inputdatatype=dict(argstr='-inputdatatype %s'), model=dict(argstr='-model %s', mandatory=True), noisemap=dict(argstr='-noisemap %s', extensions=None), out_file=dict(argstr='> %s', extensions=None, genfile=True, position=-1), outlier=dict(argstr='-outliermap %s', extensions=None), outputfile=dict(argstr='-outputfile %s', extensions=None), residualmap=dict(argstr='-residualmap %s', extensions=None), scheme_file=dict(argstr='-schemefile %s', extensions=None, mandatory=True), sigma=dict(argstr='-sigma %G'), tau=dict(argstr='-tau %G'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), bgmask=dict(argstr='-bgmask %s', extensions=None), bgthresh=dict(argstr='-bgthresh %G'), cfthresh=dict(argstr='-csfthresh %G'), environ=dict(nohash=True, usedefault=True), fixedbvalue=dict(argstr='-fixedbvalue %s'), fixedmodq=dict(argstr='-fixedmod %s'), in_file=dict(argstr='-inputfile %s', extensions=None, mandatory=True), inputdatatype=dict(argstr='-inputdatatype %s'), model=dict(argstr='-model %s', mandatory=True), noisemap=dict(argstr='-noisemap %s', extensions=None), out_file=dict(argstr='> %s', extensions=None, genfile=True, position=-1), outlier=dict(argstr='-outliermap %s', extensions=None), outputfile=dict(argstr='-outputfile %s', extensions=None), residualmap=dict(argstr='-residualmap %s', extensions=None), scheme_file=dict(argstr='-schemefile %s', extensions=None, mandatory=True), sigma=dict(argstr='-sigma %G'), tau=dict(argstr='-tau %G'))
```

## Next Steps


---

*Source: test_auto_ModelFit.py:6 | Complexity: Beginner | Last updated: 2026-05-18*