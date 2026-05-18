# How To: Affineinitializer Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test AffineInitializer inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), dimension=dict(argstr='%s', position=0, usedefault=True), environ=dict(nohash=True, usedefault=True), fixed_image=dict(argstr='%s', extensions=None, mandatory=True, position=1), local_search=dict(argstr='%d', position=7, usedefault=True), moving_image=dict(argstr='%s', extensions=None, mandatory=True, position=2), num_threads=dict(nohash=True, usedefault=True), out_file=dict(argstr='%s', extensions=None, position=3, usedefault=True), principal_axes=dict(argstr='%d', position=6, usedefault=True), radian_fraction=dict(argstr='%f', position=5, usedefault=True), search_factor=dict(argstr='%f', position=4, usedefault=True))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), dimension=dict(argstr='%s', position=0, usedefault=True), environ=dict(nohash=True, usedefault=True), fixed_image=dict(argstr='%s', extensions=None, mandatory=True, position=1), local_search=dict(argstr='%d', position=7, usedefault=True), moving_image=dict(argstr='%s', extensions=None, mandatory=True, position=2), num_threads=dict(nohash=True, usedefault=True), out_file=dict(argstr='%s', extensions=None, position=3, usedefault=True), principal_axes=dict(argstr='%d', position=6, usedefault=True), radian_fraction=dict(argstr='%f', position=5, usedefault=True), search_factor=dict(argstr='%f', position=4, usedefault=True))
```

## Next Steps


---

*Source: test_auto_AffineInitializer.py:6 | Complexity: Beginner | Last updated: 2026-05-18*