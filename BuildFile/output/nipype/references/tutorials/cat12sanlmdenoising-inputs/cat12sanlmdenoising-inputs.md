# How To: Cat12Sanlmdenoising Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test CAT12SANLMDenoising inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(addnoise=dict(field='addnoise', usedefault=True), filename_prefix=dict(field='prefix', usedefault=True), filename_suffix=dict(field='suffix', usedefault=True), in_files=dict(copyfile=False, field='data', mandatory=True), intlim=dict(field='intlim', usedefault=True), matlab_cmd=dict(), mfile=dict(usedefault=True), noisecorr_strength=dict(field='nlmfilter.optimized.NCstr', usedefault=True), paths=dict(), replace_nan_and_inf=dict(field='replaceNANandINF', usedefault=True), rician=dict(field='rician', usedefault=True), spm_type=dict(field='spm_type', usedefault=True), use_mcr=dict(), use_v8struct=dict(min_ver='8', usedefault=True))
```


## Complete Example

```python
# Workflow
input_map = dict(addnoise=dict(field='addnoise', usedefault=True), filename_prefix=dict(field='prefix', usedefault=True), filename_suffix=dict(field='suffix', usedefault=True), in_files=dict(copyfile=False, field='data', mandatory=True), intlim=dict(field='intlim', usedefault=True), matlab_cmd=dict(), mfile=dict(usedefault=True), noisecorr_strength=dict(field='nlmfilter.optimized.NCstr', usedefault=True), paths=dict(), replace_nan_and_inf=dict(field='replaceNANandINF', usedefault=True), rician=dict(field='rician', usedefault=True), spm_type=dict(field='spm_type', usedefault=True), use_mcr=dict(), use_v8struct=dict(min_ver='8', usedefault=True))
```

## Next Steps


---

*Source: test_auto_CAT12SANLMDenoising.py:6 | Complexity: Beginner | Last updated: 2026-05-18*