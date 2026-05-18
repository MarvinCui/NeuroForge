# How To: Contrast Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Contrast inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(annotation=dict(extensions=None, mandatory=True), args=dict(argstr='%s'), copy_inputs=dict(), cortex=dict(extensions=None, mandatory=True), environ=dict(nohash=True, usedefault=True), hemisphere=dict(argstr='--%s-only', mandatory=True), orig=dict(extensions=None, mandatory=True), rawavg=dict(extensions=None, mandatory=True), subject_id=dict(argstr='--s %s', mandatory=True, usedefault=True), subjects_dir=dict(), thickness=dict(extensions=None, mandatory=True), white=dict(extensions=None, mandatory=True))
```


## Complete Example

```python
# Workflow
input_map = dict(annotation=dict(extensions=None, mandatory=True), args=dict(argstr='%s'), copy_inputs=dict(), cortex=dict(extensions=None, mandatory=True), environ=dict(nohash=True, usedefault=True), hemisphere=dict(argstr='--%s-only', mandatory=True), orig=dict(extensions=None, mandatory=True), rawavg=dict(extensions=None, mandatory=True), subject_id=dict(argstr='--s %s', mandatory=True, usedefault=True), subjects_dir=dict(), thickness=dict(extensions=None, mandatory=True), white=dict(extensions=None, mandatory=True))
```

## Next Steps


---

*Source: test_auto_Contrast.py:6 | Complexity: Beginner | Last updated: 2026-05-18*