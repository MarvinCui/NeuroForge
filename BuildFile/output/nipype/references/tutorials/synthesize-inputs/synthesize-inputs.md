# How To: Synthesize Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Synthesize inputs

## Prerequisites

**Required Modules:**
- `model`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(TR=dict(argstr='-TR %f'), args=dict(argstr='%s'), cbucket=dict(argstr='-cbucket %s', copyfile=False, extensions=None, mandatory=True), cenfill=dict(argstr='-cenfill %s'), dry_run=dict(argstr='-dry'), environ=dict(nohash=True, usedefault=True), matrix=dict(argstr='-matrix %s', copyfile=False, extensions=None, mandatory=True), num_threads=dict(nohash=True, usedefault=True), out_file=dict(argstr='-prefix %s', extensions=None, name_template='syn'), outputtype=dict(), select=dict(argstr='-select %s', mandatory=True))
```


## Complete Example

```python
# Workflow
input_map = dict(TR=dict(argstr='-TR %f'), args=dict(argstr='%s'), cbucket=dict(argstr='-cbucket %s', copyfile=False, extensions=None, mandatory=True), cenfill=dict(argstr='-cenfill %s'), dry_run=dict(argstr='-dry'), environ=dict(nohash=True, usedefault=True), matrix=dict(argstr='-matrix %s', copyfile=False, extensions=None, mandatory=True), num_threads=dict(nohash=True, usedefault=True), out_file=dict(argstr='-prefix %s', extensions=None, name_template='syn'), outputtype=dict(), select=dict(argstr='-select %s', mandatory=True))
```

## Next Steps


---

*Source: test_auto_Synthesize.py:6 | Complexity: Beginner | Last updated: 2026-05-18*