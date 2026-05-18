# How To: Mrisconvert Inputs

**Difficulty**: Intermediate
**Estimated Time**: 5 minutes
**Tags**: mock

## Overview

Instantiate dict: test MRIsConvert inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(annot_file=dict(argstr='--annot %s', extensions=None), args=dict(argstr='%s'), dataarray_num=dict(argstr='--da_num %d'), environ=dict(nohash=True, usedefault=True), functional_file=dict(argstr='-f %s', extensions=None), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), label_file=dict(argstr='--label %s', extensions=None), labelstats_outfile=dict(argstr='--labelstats %s', extensions=None), normal=dict(argstr='-n'), origname=dict(argstr='-o %s'), out_datatype=dict(mandatory=True, xor=['out_file']), out_file=dict(argstr='%s', extensions=None, genfile=True, mandatory=True, position=-1, xor=['out_datatype']), parcstats_file=dict(argstr='--parcstats %s', extensions=None), patch=dict(argstr='-p'), rescale=dict(argstr='-r'), scalarcurv_file=dict(argstr='-c %s', extensions=None), scale=dict(argstr='-s %.3f'), subjects_dir=dict(), talairachxfm_subjid=dict(argstr='-t %s'), to_scanner=dict(argstr='--to-scanner'), to_tkr=dict(argstr='--to-tkr'), vertex=dict(argstr='-v'), xyz_ascii=dict(argstr='-a'))
```


## Complete Example

```python
# Workflow
input_map = dict(annot_file=dict(argstr='--annot %s', extensions=None), args=dict(argstr='%s'), dataarray_num=dict(argstr='--da_num %d'), environ=dict(nohash=True, usedefault=True), functional_file=dict(argstr='-f %s', extensions=None), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), label_file=dict(argstr='--label %s', extensions=None), labelstats_outfile=dict(argstr='--labelstats %s', extensions=None), normal=dict(argstr='-n'), origname=dict(argstr='-o %s'), out_datatype=dict(mandatory=True, xor=['out_file']), out_file=dict(argstr='%s', extensions=None, genfile=True, mandatory=True, position=-1, xor=['out_datatype']), parcstats_file=dict(argstr='--parcstats %s', extensions=None), patch=dict(argstr='-p'), rescale=dict(argstr='-r'), scalarcurv_file=dict(argstr='-c %s', extensions=None), scale=dict(argstr='-s %.3f'), subjects_dir=dict(), talairachxfm_subjid=dict(argstr='-t %s'), to_scanner=dict(argstr='--to-scanner'), to_tkr=dict(argstr='--to-tkr'), vertex=dict(argstr='-v'), xyz_ascii=dict(argstr='-a'))
```

## Next Steps


---

*Source: test_auto_MRIsConvert.py:6 | Complexity: Intermediate | Last updated: 2026-05-18*