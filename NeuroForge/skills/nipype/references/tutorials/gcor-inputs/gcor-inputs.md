# How To: Gcor Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test GCOR inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-input %s', copyfile=False, extensions=None, mandatory=True, position=-1), mask=dict(argstr='-mask %s', copyfile=False, extensions=None), nfirst=dict(argstr='-nfirst %d'), no_demean=dict(argstr='-no_demean'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-input %s', copyfile=False, extensions=None, mandatory=True, position=-1), mask=dict(argstr='-mask %s', copyfile=False, extensions=None), nfirst=dict(argstr='-nfirst %d'), no_demean=dict(argstr='-no_demean'))
```

## Next Steps


---

*Source: test_auto_GCOR.py:6 | Complexity: Beginner | Last updated: 2026-05-18*