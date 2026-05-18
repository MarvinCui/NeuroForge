# How To: Brainstalairach Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test BRAINSTalairach inputs

## Prerequisites

**Required Modules:**
- `segmentation`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(AC=dict(argstr='--AC %s', sep=','), ACisIndex=dict(argstr='--ACisIndex '), IRP=dict(argstr='--IRP %s', sep=','), IRPisIndex=dict(argstr='--IRPisIndex '), PC=dict(argstr='--PC %s', sep=','), PCisIndex=dict(argstr='--PCisIndex '), SLA=dict(argstr='--SLA %s', sep=','), SLAisIndex=dict(argstr='--SLAisIndex '), args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputVolume=dict(argstr='--inputVolume %s', extensions=None), outputBox=dict(argstr='--outputBox %s', hash_files=False), outputGrid=dict(argstr='--outputGrid %s', hash_files=False))
```


## Complete Example

```python
# Workflow
input_map = dict(AC=dict(argstr='--AC %s', sep=','), ACisIndex=dict(argstr='--ACisIndex '), IRP=dict(argstr='--IRP %s', sep=','), IRPisIndex=dict(argstr='--IRPisIndex '), PC=dict(argstr='--PC %s', sep=','), PCisIndex=dict(argstr='--PCisIndex '), SLA=dict(argstr='--SLA %s', sep=','), SLAisIndex=dict(argstr='--SLAisIndex '), args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputVolume=dict(argstr='--inputVolume %s', extensions=None), outputBox=dict(argstr='--outputBox %s', hash_files=False), outputGrid=dict(argstr='--outputGrid %s', hash_files=False))
```

## Next Steps


---

*Source: test_auto_BRAINSTalairach.py:6 | Complexity: Beginner | Last updated: 2026-05-18*