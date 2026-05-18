# How To: Brainsposteriortocontinuousclass Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test BRAINSPosteriorToContinuousClass inputs

## Prerequisites

**Required Modules:**
- `classify`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputBasalGmVolume=dict(argstr='--inputBasalGmVolume %s', extensions=None), inputCrblGmVolume=dict(argstr='--inputCrblGmVolume %s', extensions=None), inputCrblWmVolume=dict(argstr='--inputCrblWmVolume %s', extensions=None), inputCsfVolume=dict(argstr='--inputCsfVolume %s', extensions=None), inputSurfaceGmVolume=dict(argstr='--inputSurfaceGmVolume %s', extensions=None), inputVbVolume=dict(argstr='--inputVbVolume %s', extensions=None), inputWhiteVolume=dict(argstr='--inputWhiteVolume %s', extensions=None), outputVolume=dict(argstr='--outputVolume %s', hash_files=False))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputBasalGmVolume=dict(argstr='--inputBasalGmVolume %s', extensions=None), inputCrblGmVolume=dict(argstr='--inputCrblGmVolume %s', extensions=None), inputCrblWmVolume=dict(argstr='--inputCrblWmVolume %s', extensions=None), inputCsfVolume=dict(argstr='--inputCsfVolume %s', extensions=None), inputSurfaceGmVolume=dict(argstr='--inputSurfaceGmVolume %s', extensions=None), inputVbVolume=dict(argstr='--inputVbVolume %s', extensions=None), inputWhiteVolume=dict(argstr='--inputWhiteVolume %s', extensions=None), outputVolume=dict(argstr='--outputVolume %s', hash_files=False))
```

## Next Steps


---

*Source: test_auto_BRAINSPosteriorToContinuousClass.py:6 | Complexity: Beginner | Last updated: 2026-05-18*