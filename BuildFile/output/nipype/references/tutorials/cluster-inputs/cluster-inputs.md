# How To: Cluster Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Cluster inputs

## Prerequisites

**Required Modules:**
- `model`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), connectivity=dict(argstr='--connectivity=%d'), cope_file=dict(argstr='--cope=%s', extensions=None), dlh=dict(argstr='--dlh=%.10f'), environ=dict(nohash=True, usedefault=True), find_min=dict(argstr='--min', usedefault=True), fractional=dict(argstr='--fractional', usedefault=True), in_file=dict(argstr='--in=%s', extensions=None, mandatory=True), minclustersize=dict(argstr='--minclustersize', usedefault=True), no_table=dict(argstr='--no_table', usedefault=True), num_maxima=dict(argstr='--num=%d'), out_index_file=dict(argstr='--oindex=%s', hash_files=False), out_localmax_txt_file=dict(argstr='--olmax=%s', hash_files=False), out_localmax_vol_file=dict(argstr='--olmaxim=%s', hash_files=False), out_max_file=dict(argstr='--omax=%s', hash_files=False), out_mean_file=dict(argstr='--omean=%s', hash_files=False), out_pval_file=dict(argstr='--opvals=%s', hash_files=False), out_size_file=dict(argstr='--osize=%s', hash_files=False), out_threshold_file=dict(argstr='--othresh=%s', hash_files=False), output_type=dict(), peak_distance=dict(argstr='--peakdist=%.10f'), pthreshold=dict(argstr='--pthresh=%.10f', requires=['dlh', 'volume']), std_space_file=dict(argstr='--stdvol=%s', extensions=None), threshold=dict(argstr='--thresh=%.10f', mandatory=True), use_mm=dict(argstr='--mm', usedefault=True), volume=dict(argstr='--volume=%d'), warpfield_file=dict(argstr='--warpvol=%s', extensions=None), xfm_file=dict(argstr='--xfm=%s', extensions=None))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), connectivity=dict(argstr='--connectivity=%d'), cope_file=dict(argstr='--cope=%s', extensions=None), dlh=dict(argstr='--dlh=%.10f'), environ=dict(nohash=True, usedefault=True), find_min=dict(argstr='--min', usedefault=True), fractional=dict(argstr='--fractional', usedefault=True), in_file=dict(argstr='--in=%s', extensions=None, mandatory=True), minclustersize=dict(argstr='--minclustersize', usedefault=True), no_table=dict(argstr='--no_table', usedefault=True), num_maxima=dict(argstr='--num=%d'), out_index_file=dict(argstr='--oindex=%s', hash_files=False), out_localmax_txt_file=dict(argstr='--olmax=%s', hash_files=False), out_localmax_vol_file=dict(argstr='--olmaxim=%s', hash_files=False), out_max_file=dict(argstr='--omax=%s', hash_files=False), out_mean_file=dict(argstr='--omean=%s', hash_files=False), out_pval_file=dict(argstr='--opvals=%s', hash_files=False), out_size_file=dict(argstr='--osize=%s', hash_files=False), out_threshold_file=dict(argstr='--othresh=%s', hash_files=False), output_type=dict(), peak_distance=dict(argstr='--peakdist=%.10f'), pthreshold=dict(argstr='--pthresh=%.10f', requires=['dlh', 'volume']), std_space_file=dict(argstr='--stdvol=%s', extensions=None), threshold=dict(argstr='--thresh=%.10f', mandatory=True), use_mm=dict(argstr='--mm', usedefault=True), volume=dict(argstr='--volume=%d'), warpfield_file=dict(argstr='--warpvol=%s', extensions=None), xfm_file=dict(argstr='--xfm=%s', extensions=None))
```

## Next Steps


---

*Source: test_auto_Cluster.py:6 | Complexity: Beginner | Last updated: 2026-05-18*