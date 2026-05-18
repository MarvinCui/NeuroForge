# How To: Eslr Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test ESLR inputs

## Prerequisites

**Required Modules:**
- `specialized`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), closingSize=dict(argstr='--closingSize %d'), environ=dict(nohash=True, usedefault=True), high=dict(argstr='--high %d'), inputVolume=dict(argstr='--inputVolume %s', extensions=None), low=dict(argstr='--low %d'), numberOfThreads=dict(argstr='--numberOfThreads %d'), openingSize=dict(argstr='--openingSize %d'), outputVolume=dict(argstr='--outputVolume %s', hash_files=False), preserveOutside=dict(argstr='--preserveOutside '), safetySize=dict(argstr='--safetySize %d'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), closingSize=dict(argstr='--closingSize %d'), environ=dict(nohash=True, usedefault=True), high=dict(argstr='--high %d'), inputVolume=dict(argstr='--inputVolume %s', extensions=None), low=dict(argstr='--low %d'), numberOfThreads=dict(argstr='--numberOfThreads %d'), openingSize=dict(argstr='--openingSize %d'), outputVolume=dict(argstr='--outputVolume %s', hash_files=False), preserveOutside=dict(argstr='--preserveOutside '), safetySize=dict(argstr='--safetySize %d'))
```

## Next Steps


---

*Source: test_auto_ESLR.py:6 | Complexity: Beginner | Last updated: 2026-05-18*