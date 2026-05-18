# How To: Brainstalairachmask Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test BRAINSTalairachMask inputs

## Prerequisites

**Required Modules:**
- `segmentation`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), expand=dict(argstr='--expand '), hemisphereMode=dict(argstr='--hemisphereMode %s'), inputVolume=dict(argstr='--inputVolume %s', extensions=None), outputVolume=dict(argstr='--outputVolume %s', hash_files=False), talairachBox=dict(argstr='--talairachBox %s', extensions=None), talairachParameters=dict(argstr='--talairachParameters %s', extensions=None))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), expand=dict(argstr='--expand '), hemisphereMode=dict(argstr='--hemisphereMode %s'), inputVolume=dict(argstr='--inputVolume %s', extensions=None), outputVolume=dict(argstr='--outputVolume %s', hash_files=False), talairachBox=dict(argstr='--talairachBox %s', extensions=None), talairachParameters=dict(argstr='--talairachParameters %s', extensions=None))
```

## Next Steps


---

*Source: test_auto_BRAINSTalairachMask.py:6 | Complexity: Beginner | Last updated: 2026-05-18*