# How To: Analyzewarp Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test AnalyzeWarp inputs

## Prerequisites

**Required Modules:**
- `registration`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), jac=dict(argstr='-jac %s', usedefault=True), jacmat=dict(argstr='-jacmat %s', usedefault=True), moving_image=dict(argstr='-in %s', extensions=None), num_threads=dict(argstr='-threads %01d', nohash=True, usedefault=True), output_path=dict(argstr='-out %s', mandatory=True, usedefault=True), points=dict(argstr='-def %s', position=0, usedefault=True), transform_file=dict(argstr='-tp %s', extensions=None, mandatory=True))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), jac=dict(argstr='-jac %s', usedefault=True), jacmat=dict(argstr='-jacmat %s', usedefault=True), moving_image=dict(argstr='-in %s', extensions=None), num_threads=dict(argstr='-threads %01d', nohash=True, usedefault=True), output_path=dict(argstr='-out %s', mandatory=True, usedefault=True), points=dict(argstr='-def %s', position=0, usedefault=True), transform_file=dict(argstr='-tp %s', extensions=None, mandatory=True))
```

## Next Steps


---

*Source: test_auto_AnalyzeWarp.py:6 | Complexity: Beginner | Last updated: 2026-05-18*