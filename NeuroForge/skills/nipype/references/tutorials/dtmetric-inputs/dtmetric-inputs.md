# How To: Dtmetric Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test DTMetric inputs

## Prerequisites

**Required Modules:**
- `dti`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), data_header=dict(argstr='-header %s', extensions=None), eigen_data=dict(argstr='-inputfile %s', extensions=None, mandatory=True), environ=dict(nohash=True, usedefault=True), inputdatatype=dict(argstr='-inputdatatype %s', usedefault=True), metric=dict(argstr='-stat %s', mandatory=True), outputdatatype=dict(argstr='-outputdatatype %s', usedefault=True), outputfile=dict(argstr='-outputfile %s', extensions=None, genfile=True))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), data_header=dict(argstr='-header %s', extensions=None), eigen_data=dict(argstr='-inputfile %s', extensions=None, mandatory=True), environ=dict(nohash=True, usedefault=True), inputdatatype=dict(argstr='-inputdatatype %s', usedefault=True), metric=dict(argstr='-stat %s', mandatory=True), outputdatatype=dict(argstr='-outputdatatype %s', usedefault=True), outputfile=dict(argstr='-outputfile %s', extensions=None, genfile=True))
```

## Next Steps


---

*Source: test_auto_DTMetric.py:6 | Complexity: Beginner | Last updated: 2026-05-18*