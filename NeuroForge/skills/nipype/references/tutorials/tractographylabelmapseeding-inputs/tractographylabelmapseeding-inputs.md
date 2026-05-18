# How To: Tractographylabelmapseeding Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test TractographyLabelMapSeeding inputs

## Prerequisites

**Required Modules:**
- `diffusion`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(InputVolume=dict(argstr='%s', extensions=None, position=-2), OutputFibers=dict(argstr='%s', hash_files=False, position=-1), args=dict(argstr='%s'), clthreshold=dict(argstr='--clthreshold %f'), environ=dict(nohash=True, usedefault=True), inputroi=dict(argstr='--inputroi %s', extensions=None), integrationsteplength=dict(argstr='--integrationsteplength %f'), label=dict(argstr='--label %d'), maximumlength=dict(argstr='--maximumlength %f'), minimumlength=dict(argstr='--minimumlength %f'), name=dict(argstr='--name %s'), outputdirectory=dict(argstr='--outputdirectory %s', hash_files=False), randomgrid=dict(argstr='--randomgrid '), seedspacing=dict(argstr='--seedspacing %f'), stoppingcurvature=dict(argstr='--stoppingcurvature %f'), stoppingmode=dict(argstr='--stoppingmode %s'), stoppingvalue=dict(argstr='--stoppingvalue %f'), useindexspace=dict(argstr='--useindexspace '), writetofile=dict(argstr='--writetofile '))
```


## Complete Example

```python
# Workflow
input_map = dict(InputVolume=dict(argstr='%s', extensions=None, position=-2), OutputFibers=dict(argstr='%s', hash_files=False, position=-1), args=dict(argstr='%s'), clthreshold=dict(argstr='--clthreshold %f'), environ=dict(nohash=True, usedefault=True), inputroi=dict(argstr='--inputroi %s', extensions=None), integrationsteplength=dict(argstr='--integrationsteplength %f'), label=dict(argstr='--label %d'), maximumlength=dict(argstr='--maximumlength %f'), minimumlength=dict(argstr='--minimumlength %f'), name=dict(argstr='--name %s'), outputdirectory=dict(argstr='--outputdirectory %s', hash_files=False), randomgrid=dict(argstr='--randomgrid '), seedspacing=dict(argstr='--seedspacing %f'), stoppingcurvature=dict(argstr='--stoppingcurvature %f'), stoppingmode=dict(argstr='--stoppingmode %s'), stoppingvalue=dict(argstr='--stoppingvalue %f'), useindexspace=dict(argstr='--useindexspace '), writetofile=dict(argstr='--writetofile '))
```

## Next Steps


---

*Source: test_auto_TractographyLabelMapSeeding.py:6 | Complexity: Beginner | Last updated: 2026-05-18*