# How To: Makeaveragesubject Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test MakeAverageSubject inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), out_name=dict(argstr='--out %s', extensions=None, usedefault=True), subjects_dir=dict(), subjects_ids=dict(argstr='--subjects %s', mandatory=True, sep=' '))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), out_name=dict(argstr='--out %s', extensions=None, usedefault=True), subjects_dir=dict(), subjects_ids=dict(argstr='--subjects %s', mandatory=True, sep=' '))
```

## Next Steps


---

*Source: test_auto_MakeAverageSubject.py:6 | Complexity: Beginner | Last updated: 2026-05-18*