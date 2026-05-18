# How To: Hammerattributecreator Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test HammerAttributeCreator inputs

## Prerequisites

**Required Modules:**
- `featuredetection`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(Scale=dict(argstr='--Scale %d'), Strength=dict(argstr='--Strength %f'), args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputCSFVolume=dict(argstr='--inputCSFVolume %s', extensions=None), inputGMVolume=dict(argstr='--inputGMVolume %s', extensions=None), inputWMVolume=dict(argstr='--inputWMVolume %s', extensions=None), outputVolumeBase=dict(argstr='--outputVolumeBase %s'))
```


## Complete Example

```python
# Workflow
input_map = dict(Scale=dict(argstr='--Scale %d'), Strength=dict(argstr='--Strength %f'), args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputCSFVolume=dict(argstr='--inputCSFVolume %s', extensions=None), inputGMVolume=dict(argstr='--inputGMVolume %s', extensions=None), inputWMVolume=dict(argstr='--inputWMVolume %s', extensions=None), outputVolumeBase=dict(argstr='--outputVolumeBase %s'))
```

## Next Steps


---

*Source: test_auto_HammerAttributeCreator.py:6 | Complexity: Beginner | Last updated: 2026-05-18*