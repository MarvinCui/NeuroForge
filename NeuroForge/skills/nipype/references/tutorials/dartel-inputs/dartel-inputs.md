# How To: Dartel Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test DARTEL inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(image_files=dict(copyfile=False, field='warp.images', mandatory=True), iteration_parameters=dict(field='warp.settings.param'), matlab_cmd=dict(), mfile=dict(usedefault=True), optimization_parameters=dict(field='warp.settings.optim'), paths=dict(), regularization_form=dict(field='warp.settings.rform'), template_prefix=dict(field='warp.settings.template', usedefault=True), use_mcr=dict(), use_v8struct=dict(min_ver='8', usedefault=True))
```


## Complete Example

```python
# Workflow
input_map = dict(image_files=dict(copyfile=False, field='warp.images', mandatory=True), iteration_parameters=dict(field='warp.settings.param'), matlab_cmd=dict(), mfile=dict(usedefault=True), optimization_parameters=dict(field='warp.settings.optim'), paths=dict(), regularization_form=dict(field='warp.settings.rform'), template_prefix=dict(field='warp.settings.template', usedefault=True), use_mcr=dict(), use_v8struct=dict(min_ver='8', usedefault=True))
```

## Next Steps


---

*Source: test_auto_DARTEL.py:6 | Complexity: Beginner | Last updated: 2026-05-18*