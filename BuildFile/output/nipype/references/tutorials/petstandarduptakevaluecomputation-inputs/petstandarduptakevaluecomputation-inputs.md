# How To: Petstandarduptakevaluecomputation Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test PETStandardUptakeValueComputation inputs

## Prerequisites

**Required Modules:**
- `petstandarduptakevaluecomputation`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(OutputLabel=dict(argstr='--OutputLabel %s'), OutputLabelValue=dict(argstr='--OutputLabelValue %s'), SUVMax=dict(argstr='--SUVMax %s'), SUVMean=dict(argstr='--SUVMean %s'), SUVMin=dict(argstr='--SUVMin %s'), args=dict(argstr='%s'), color=dict(argstr='--color %s', extensions=None), csvFile=dict(argstr='--csvFile %s', hash_files=False), environ=dict(nohash=True, usedefault=True), labelMap=dict(argstr='--labelMap %s', extensions=None), petDICOMPath=dict(argstr='--petDICOMPath %s'), petVolume=dict(argstr='--petVolume %s', extensions=None))
```


## Complete Example

```python
# Workflow
input_map = dict(OutputLabel=dict(argstr='--OutputLabel %s'), OutputLabelValue=dict(argstr='--OutputLabelValue %s'), SUVMax=dict(argstr='--SUVMax %s'), SUVMean=dict(argstr='--SUVMean %s'), SUVMin=dict(argstr='--SUVMin %s'), args=dict(argstr='%s'), color=dict(argstr='--color %s', extensions=None), csvFile=dict(argstr='--csvFile %s', hash_files=False), environ=dict(nohash=True, usedefault=True), labelMap=dict(argstr='--labelMap %s', extensions=None), petDICOMPath=dict(argstr='--petDICOMPath %s'), petVolume=dict(argstr='--petVolume %s', extensions=None))
```

## Next Steps


---

*Source: test_auto_PETStandardUptakeValueComputation.py:6 | Complexity: Beginner | Last updated: 2026-05-18*