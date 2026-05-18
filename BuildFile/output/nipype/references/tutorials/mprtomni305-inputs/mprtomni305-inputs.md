# How To: Mprtomni305 Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test MPRtoMNI305 inputs

## Prerequisites

**Required Modules:**
- `registration`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, usedefault=True), reference_dir=dict(mandatory=True, usedefault=True), subjects_dir=dict(), target=dict(mandatory=True, usedefault=True))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, usedefault=True), reference_dir=dict(mandatory=True, usedefault=True), subjects_dir=dict(), target=dict(mandatory=True, usedefault=True))
```

## Next Steps


---

*Source: test_auto_MPRtoMNI305.py:6 | Complexity: Beginner | Last updated: 2026-05-18*