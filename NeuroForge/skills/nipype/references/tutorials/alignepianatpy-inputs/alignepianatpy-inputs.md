# How To: Alignepianatpy Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test AlignEpiAnatPy inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(anat=dict(argstr='-anat %s', copyfile=False, extensions=None, mandatory=True), anat2epi=dict(argstr='-anat2epi'), args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), epi2anat=dict(argstr='-epi2anat'), epi_base=dict(argstr='-epi_base %s', mandatory=True), epi_strip=dict(argstr='-epi_strip %s'), in_file=dict(argstr='-epi %s', copyfile=False, extensions=None, mandatory=True), outputtype=dict(), py27_path=dict(usedefault=True), save_skullstrip=dict(argstr='-save_skullstrip'), suffix=dict(argstr='-suffix %s', usedefault=True), tshift=dict(argstr='-tshift %s', usedefault=True), volreg=dict(argstr='-volreg %s', usedefault=True))
```


## Complete Example

```python
# Workflow
input_map = dict(anat=dict(argstr='-anat %s', copyfile=False, extensions=None, mandatory=True), anat2epi=dict(argstr='-anat2epi'), args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), epi2anat=dict(argstr='-epi2anat'), epi_base=dict(argstr='-epi_base %s', mandatory=True), epi_strip=dict(argstr='-epi_strip %s'), in_file=dict(argstr='-epi %s', copyfile=False, extensions=None, mandatory=True), outputtype=dict(), py27_path=dict(usedefault=True), save_skullstrip=dict(argstr='-save_skullstrip'), suffix=dict(argstr='-suffix %s', usedefault=True), tshift=dict(argstr='-tshift %s', usedefault=True), volreg=dict(argstr='-volreg %s', usedefault=True))
```

## Next Steps


---

*Source: test_auto_AlignEpiAnatPy.py:6 | Complexity: Beginner | Last updated: 2026-05-18*