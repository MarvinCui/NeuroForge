# How To: Gtractcreateguidefiber Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test gtractCreateGuideFiber inputs

## Prerequisites

**Required Modules:**
- `gtract`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputFiber=dict(argstr='--inputFiber %s', extensions=None), numberOfPoints=dict(argstr='--numberOfPoints %d'), numberOfThreads=dict(argstr='--numberOfThreads %d'), outputFiber=dict(argstr='--outputFiber %s', hash_files=False), writeXMLPolyDataFile=dict(argstr='--writeXMLPolyDataFile '))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputFiber=dict(argstr='--inputFiber %s', extensions=None), numberOfPoints=dict(argstr='--numberOfPoints %d'), numberOfThreads=dict(argstr='--numberOfThreads %d'), outputFiber=dict(argstr='--outputFiber %s', hash_files=False), writeXMLPolyDataFile=dict(argstr='--writeXMLPolyDataFile '))
```

## Next Steps


---

*Source: test_auto_gtractCreateGuideFiber.py:6 | Complexity: Beginner | Last updated: 2026-05-18*