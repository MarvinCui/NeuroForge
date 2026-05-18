# How To: Notes Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Notes inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(add=dict(argstr='-a "%s"'), add_history=dict(argstr='-h "%s"', xor=['rep_history']), args=dict(argstr='%s'), delete=dict(argstr='-d %d'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', copyfile=False, extensions=None, mandatory=True, position=-1), num_threads=dict(nohash=True, usedefault=True), out_file=dict(argstr='%s', extensions=None), outputtype=dict(), rep_history=dict(argstr='-HH "%s"', xor=['add_history']), ses=dict(argstr='-ses'))
```


## Complete Example

```python
# Workflow
input_map = dict(add=dict(argstr='-a "%s"'), add_history=dict(argstr='-h "%s"', xor=['rep_history']), args=dict(argstr='%s'), delete=dict(argstr='-d %d'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', copyfile=False, extensions=None, mandatory=True, position=-1), num_threads=dict(nohash=True, usedefault=True), out_file=dict(argstr='%s', extensions=None), outputtype=dict(), rep_history=dict(argstr='-HH "%s"', xor=['add_history']), ses=dict(argstr='-ses'))
```

## Next Steps


---

*Source: test_auto_Notes.py:6 | Complexity: Beginner | Last updated: 2026-05-18*