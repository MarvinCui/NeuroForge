# How To: Matlabcommand Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test MatlabCommand inputs

## Prerequisites

**Required Modules:**
- `matlab`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), logfile=dict(argstr='-logfile %s', extensions=None), mfile=dict(usedefault=True), nodesktop=dict(argstr='-nodesktop', nohash=True, usedefault=True), nosplash=dict(argstr='-nosplash', nohash=True, usedefault=True), paths=dict(), postscript=dict(usedefault=True), prescript=dict(usedefault=True), script=dict(argstr='-r "%s;exit"', mandatory=True, position=-1), script_file=dict(extensions=None, usedefault=True), single_comp_thread=dict(argstr='-singleCompThread', nohash=True), uses_mcr=dict(nohash=True, xor=['nodesktop', 'nosplash', 'single_comp_thread']))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), logfile=dict(argstr='-logfile %s', extensions=None), mfile=dict(usedefault=True), nodesktop=dict(argstr='-nodesktop', nohash=True, usedefault=True), nosplash=dict(argstr='-nosplash', nohash=True, usedefault=True), paths=dict(), postscript=dict(usedefault=True), prescript=dict(usedefault=True), script=dict(argstr='-r "%s;exit"', mandatory=True, position=-1), script_file=dict(extensions=None, usedefault=True), single_comp_thread=dict(argstr='-singleCompThread', nohash=True), uses_mcr=dict(nohash=True, xor=['nodesktop', 'nosplash', 'single_comp_thread']))
```

## Next Steps


---

*Source: test_auto_MatlabCommand.py:6 | Complexity: Beginner | Last updated: 2026-05-18*