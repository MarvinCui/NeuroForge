# How To: Buildtemplateparallel Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test buildtemplateparallel inputs

## Prerequisites

**Required Modules:**
- `legacy`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), bias_field_correction=dict(argstr='-n 1'), dimension=dict(argstr='-d %d', position=1, usedefault=True), environ=dict(nohash=True, usedefault=True), gradient_step_size=dict(argstr='-g %f'), in_files=dict(argstr='%s', mandatory=True, position=-1), iteration_limit=dict(argstr='-i %d', usedefault=True), max_iterations=dict(argstr='-m %s', sep='x'), num_cores=dict(argstr='-j %d', requires=['parallelization']), num_threads=dict(nohash=True, usedefault=True), out_prefix=dict(argstr='-o %s', usedefault=True), parallelization=dict(argstr='-c %d', usedefault=True), rigid_body_registration=dict(argstr='-r 1'), similarity_metric=dict(argstr='-s %s'), transformation_model=dict(argstr='-t %s', usedefault=True), use_first_as_target=dict())
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), bias_field_correction=dict(argstr='-n 1'), dimension=dict(argstr='-d %d', position=1, usedefault=True), environ=dict(nohash=True, usedefault=True), gradient_step_size=dict(argstr='-g %f'), in_files=dict(argstr='%s', mandatory=True, position=-1), iteration_limit=dict(argstr='-i %d', usedefault=True), max_iterations=dict(argstr='-m %s', sep='x'), num_cores=dict(argstr='-j %d', requires=['parallelization']), num_threads=dict(nohash=True, usedefault=True), out_prefix=dict(argstr='-o %s', usedefault=True), parallelization=dict(argstr='-c %d', usedefault=True), rigid_body_registration=dict(argstr='-r 1'), similarity_metric=dict(argstr='-s %s'), transformation_model=dict(argstr='-t %s', usedefault=True), use_first_as_target=dict())
```

## Next Steps


---

*Source: test_auto_buildtemplateparallel.py:6 | Complexity: Beginner | Last updated: 2026-05-18*