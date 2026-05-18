# How To: Autotlrc Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test AutoTLRC inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), base=dict(argstr='-base %s', mandatory=True), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-input %s', copyfile=False, extensions=None, mandatory=True), no_ss=dict(argstr='-no_ss'), outputtype=dict())
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), base=dict(argstr='-base %s', mandatory=True), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-input %s', copyfile=False, extensions=None, mandatory=True), no_ss=dict(argstr='-no_ss'), outputtype=dict())
```

## Next Steps


---

*Source: test_auto_AutoTLRC.py:6 | Complexity: Beginner | Last updated: 2026-05-18*