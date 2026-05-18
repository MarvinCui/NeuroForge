# How To: Gtractresamplefibers Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test gtractResampleFibers inputs

## Prerequisites

**Required Modules:**
- `gtract`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputForwardDeformationFieldVolume=dict(argstr='--inputForwardDeformationFieldVolume %s', extensions=None), inputReverseDeformationFieldVolume=dict(argstr='--inputReverseDeformationFieldVolume %s', extensions=None), inputTract=dict(argstr='--inputTract %s', extensions=None), numberOfThreads=dict(argstr='--numberOfThreads %d'), outputTract=dict(argstr='--outputTract %s', hash_files=False), writeXMLPolyDataFile=dict(argstr='--writeXMLPolyDataFile '))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inputForwardDeformationFieldVolume=dict(argstr='--inputForwardDeformationFieldVolume %s', extensions=None), inputReverseDeformationFieldVolume=dict(argstr='--inputReverseDeformationFieldVolume %s', extensions=None), inputTract=dict(argstr='--inputTract %s', extensions=None), numberOfThreads=dict(argstr='--numberOfThreads %d'), outputTract=dict(argstr='--outputTract %s', hash_files=False), writeXMLPolyDataFile=dict(argstr='--writeXMLPolyDataFile '))
```

## Next Steps


---

*Source: test_auto_gtractResampleFibers.py:6 | Complexity: Beginner | Last updated: 2026-05-18*