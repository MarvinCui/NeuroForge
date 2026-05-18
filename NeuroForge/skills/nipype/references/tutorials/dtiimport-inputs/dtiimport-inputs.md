# How To: Dtiimport Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test DTIimport inputs

## Prerequisites

**Required Modules:**
- `diffusion`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputFile=dict(argstr='%s', extensions=None, position=-2), outputTensor=dict(argstr='%s', hash_files=False, position=-1), testingmode=dict(argstr='--testingmode '))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputFile=dict(argstr='%s', extensions=None, position=-2), outputTensor=dict(argstr='%s', hash_files=False, position=-1), testingmode=dict(argstr='--testingmode '))
```

## Next Steps


---

*Source: test_auto_DTIimport.py:6 | Complexity: Beginner | Last updated: 2026-05-18*