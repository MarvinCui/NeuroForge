# How To: Svreg Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test SVReg inputs

## Prerequisites

**Required Modules:**
- `brainsuite`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), atlasFilePrefix=dict(argstr="'%s'", position=1), curveMatchingInstructions=dict(argstr="'-cur %s'"), dataSinkDelay=dict(argstr='%s'), displayModuleName=dict(argstr="'-m'"), displayTimestamps=dict(argstr="'-t'"), environ=dict(nohash=True, usedefault=True), iterations=dict(argstr="'-H %d'"), keepIntermediates=dict(argstr="'-k'"), pialSurfaceMaskDilation=dict(argstr="'-D %d'"), refineOutputs=dict(argstr="'-r'"), shortMessages=dict(argstr="'-gui'"), skipToIntensityReg=dict(argstr="'-p'"), skipToVolumeReg=dict(argstr="'-s'"), skipVolumetricProcessing=dict(argstr="'-S'"), subjectFilePrefix=dict(argstr="'%s'", mandatory=True, position=0), useCerebrumMask=dict(argstr="'-C'"), useManualMaskFile=dict(argstr="'-cbm'"), useMultiThreading=dict(argstr="'-P'"), useSingleThreading=dict(argstr="'-U'"), verbosity0=dict(argstr="'-v0'", xor=('verbosity0', 'verbosity1', 'verbosity2')), verbosity1=dict(argstr="'-v1'", xor=('verbosity0', 'verbosity1', 'verbosity2')), verbosity2=dict(argstr="'v2'", xor=('verbosity0', 'verbosity1', 'verbosity2')))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), atlasFilePrefix=dict(argstr="'%s'", position=1), curveMatchingInstructions=dict(argstr="'-cur %s'"), dataSinkDelay=dict(argstr='%s'), displayModuleName=dict(argstr="'-m'"), displayTimestamps=dict(argstr="'-t'"), environ=dict(nohash=True, usedefault=True), iterations=dict(argstr="'-H %d'"), keepIntermediates=dict(argstr="'-k'"), pialSurfaceMaskDilation=dict(argstr="'-D %d'"), refineOutputs=dict(argstr="'-r'"), shortMessages=dict(argstr="'-gui'"), skipToIntensityReg=dict(argstr="'-p'"), skipToVolumeReg=dict(argstr="'-s'"), skipVolumetricProcessing=dict(argstr="'-S'"), subjectFilePrefix=dict(argstr="'%s'", mandatory=True, position=0), useCerebrumMask=dict(argstr="'-C'"), useManualMaskFile=dict(argstr="'-cbm'"), useMultiThreading=dict(argstr="'-P'"), useSingleThreading=dict(argstr="'-U'"), verbosity0=dict(argstr="'-v0'", xor=('verbosity0', 'verbosity1', 'verbosity2')), verbosity1=dict(argstr="'-v1'", xor=('verbosity0', 'verbosity1', 'verbosity2')), verbosity2=dict(argstr="'v2'", xor=('verbosity0', 'verbosity1', 'verbosity2')))
```

## Next Steps


---

*Source: test_auto_SVReg.py:6 | Complexity: Beginner | Last updated: 2026-05-18*