# How To: Procstreamlines Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test ProcStreamlines inputs

## Prerequisites

**Required Modules:**
- `convert`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(allowmultitargets=dict(argstr='-allowmultitargets'), args=dict(argstr='%s'), datadims=dict(argstr='-datadims %s', units='voxels'), directional=dict(argstr='-directional %s', units='NA'), discardloops=dict(argstr='-discardloops'), endpointfile=dict(argstr='-endpointfile %s', extensions=None), environ=dict(nohash=True, usedefault=True), exclusionfile=dict(argstr='-exclusionfile %s', extensions=None), gzip=dict(argstr='-gzip'), in_file=dict(argstr='-inputfile %s', extensions=None, mandatory=True, position=1), inputmodel=dict(argstr='-inputmodel %s', usedefault=True), iterations=dict(argstr='-iterations %d', units='NA'), maxtractlength=dict(argstr='-maxtractlength %d', units='mm'), maxtractpoints=dict(argstr='-maxtractpoints %d', units='NA'), mintractlength=dict(argstr='-mintractlength %d', units='mm'), mintractpoints=dict(argstr='-mintractpoints %d', units='NA'), noresample=dict(argstr='-noresample'), out_file=dict(argstr='> %s', extensions=None, genfile=True, position=-1), outputacm=dict(argstr='-outputacm', requires=['outputroot', 'seedfile']), outputcbs=dict(argstr='-outputcbs', requires=['outputroot', 'targetfile', 'seedfile']), outputcp=dict(argstr='-outputcp', requires=['outputroot', 'seedfile']), outputroot=dict(argstr='-outputroot %s', extensions=None), outputsc=dict(argstr='-outputsc', requires=['outputroot', 'seedfile']), outputtracts=dict(argstr='-outputtracts'), regionindex=dict(argstr='-regionindex %d', units='mm'), resamplestepsize=dict(argstr='-resamplestepsize %d', units='NA'), seedfile=dict(argstr='-seedfile %s', extensions=None), seedpointmm=dict(argstr='-seedpointmm %s', units='mm'), seedpointvox=dict(argstr='-seedpointvox %s', units='voxels'), targetfile=dict(argstr='-targetfile %s', extensions=None), truncateinexclusion=dict(argstr='-truncateinexclusion'), truncateloops=dict(argstr='-truncateloops'), voxeldims=dict(argstr='-voxeldims %s', units='mm'), waypointfile=dict(argstr='-waypointfile %s', extensions=None))
```


## Complete Example

```python
# Workflow
input_map = dict(allowmultitargets=dict(argstr='-allowmultitargets'), args=dict(argstr='%s'), datadims=dict(argstr='-datadims %s', units='voxels'), directional=dict(argstr='-directional %s', units='NA'), discardloops=dict(argstr='-discardloops'), endpointfile=dict(argstr='-endpointfile %s', extensions=None), environ=dict(nohash=True, usedefault=True), exclusionfile=dict(argstr='-exclusionfile %s', extensions=None), gzip=dict(argstr='-gzip'), in_file=dict(argstr='-inputfile %s', extensions=None, mandatory=True, position=1), inputmodel=dict(argstr='-inputmodel %s', usedefault=True), iterations=dict(argstr='-iterations %d', units='NA'), maxtractlength=dict(argstr='-maxtractlength %d', units='mm'), maxtractpoints=dict(argstr='-maxtractpoints %d', units='NA'), mintractlength=dict(argstr='-mintractlength %d', units='mm'), mintractpoints=dict(argstr='-mintractpoints %d', units='NA'), noresample=dict(argstr='-noresample'), out_file=dict(argstr='> %s', extensions=None, genfile=True, position=-1), outputacm=dict(argstr='-outputacm', requires=['outputroot', 'seedfile']), outputcbs=dict(argstr='-outputcbs', requires=['outputroot', 'targetfile', 'seedfile']), outputcp=dict(argstr='-outputcp', requires=['outputroot', 'seedfile']), outputroot=dict(argstr='-outputroot %s', extensions=None), outputsc=dict(argstr='-outputsc', requires=['outputroot', 'seedfile']), outputtracts=dict(argstr='-outputtracts'), regionindex=dict(argstr='-regionindex %d', units='mm'), resamplestepsize=dict(argstr='-resamplestepsize %d', units='NA'), seedfile=dict(argstr='-seedfile %s', extensions=None), seedpointmm=dict(argstr='-seedpointmm %s', units='mm'), seedpointvox=dict(argstr='-seedpointvox %s', units='voxels'), targetfile=dict(argstr='-targetfile %s', extensions=None), truncateinexclusion=dict(argstr='-truncateinexclusion'), truncateloops=dict(argstr='-truncateloops'), voxeldims=dict(argstr='-voxeldims %s', units='mm'), waypointfile=dict(argstr='-waypointfile %s', extensions=None))
```

## Next Steps


---

*Source: test_auto_ProcStreamlines.py:6 | Complexity: Beginner | Last updated: 2026-05-18*