# How To: Realign Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Realign inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(fwhm=dict(field='eoptions.fwhm'), in_files=dict(copyfile=True, field='data', mandatory=True), interp=dict(field='eoptions.interp'), jobtype=dict(usedefault=True), matlab_cmd=dict(), mfile=dict(usedefault=True), out_prefix=dict(field='roptions.prefix', usedefault=True), paths=dict(), quality=dict(field='eoptions.quality'), register_to_mean=dict(field='eoptions.rtm'), separation=dict(field='eoptions.sep'), use_mcr=dict(), use_v8struct=dict(min_ver='8', usedefault=True), weight_img=dict(extensions=None, field='eoptions.weight'), wrap=dict(field='eoptions.wrap'), write_interp=dict(field='roptions.interp'), write_mask=dict(field='roptions.mask'), write_which=dict(field='roptions.which', usedefault=True), write_wrap=dict(field='roptions.wrap'))
```


## Complete Example

```python
# Workflow
input_map = dict(fwhm=dict(field='eoptions.fwhm'), in_files=dict(copyfile=True, field='data', mandatory=True), interp=dict(field='eoptions.interp'), jobtype=dict(usedefault=True), matlab_cmd=dict(), mfile=dict(usedefault=True), out_prefix=dict(field='roptions.prefix', usedefault=True), paths=dict(), quality=dict(field='eoptions.quality'), register_to_mean=dict(field='eoptions.rtm'), separation=dict(field='eoptions.sep'), use_mcr=dict(), use_v8struct=dict(min_ver='8', usedefault=True), weight_img=dict(extensions=None, field='eoptions.weight'), wrap=dict(field='eoptions.wrap'), write_interp=dict(field='roptions.interp'), write_mask=dict(field='roptions.mask'), write_which=dict(field='roptions.which', usedefault=True), write_wrap=dict(field='roptions.wrap'))
```

## Next Steps


---

*Source: test_auto_Realign.py:6 | Complexity: Beginner | Last updated: 2026-05-18*