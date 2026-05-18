# How To: Applywarp

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test applywarp

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `copy`
- `pytest`
- `nipype.utils.filemanip`
- `nipype.interfaces.fsl`
- `nipype.interfaces.base`
- `nipype.interfaces.fsl`
- `nibabel`
- `numpy`
- `os.path`

**Setup Required:**
```python
# Fixtures: setup_flirt
```

## Step-by-Step Guide

### Step 1: Assign unknown = setup_flirt

```python
tmpdir, infile, reffile = setup_flirt
```

**Verification:**
```python
assert awarp.cmdline == realcmd
```

### Step 2: Assign opt_map = value

```python
opt_map = {'out_file': ('--out=bar.nii', 'bar.nii'), 'premat': ('--premat=%s' % reffile, reffile), 'postmat': ('--postmat=%s' % reffile, reffile)}
```

### Step 3: Assign awarp = fsl.ApplyWarp(...)

```python
awarp = fsl.ApplyWarp(in_file=infile, ref_file=reffile, field_file=reffile, **{name: settings[1]})
```

**Verification:**
```python
assert awarp.cmdline == realcmd
```

### Step 4: Assign realcmd = value

```python
realcmd = 'applywarp --in=%s --ref=%s --out=%s --warp=%s' % (infile, reffile, settings[1], reffile)
```

### Step 5: Assign outfile = awarp._gen_fname(...)

```python
outfile = awarp._gen_fname(infile, suffix='_warp')
```

### Step 6: Assign realcmd = value

```python
realcmd = 'applywarp --in=%s --ref=%s --out=%s --warp=%s %s' % (infile, reffile, outfile, reffile, settings[0])
```


## Complete Example

```python
# Setup
# Fixtures: setup_flirt

# Workflow
tmpdir, infile, reffile = setup_flirt
opt_map = {'out_file': ('--out=bar.nii', 'bar.nii'), 'premat': ('--premat=%s' % reffile, reffile), 'postmat': ('--postmat=%s' % reffile, reffile)}
for name, settings in list(opt_map.items()):
    awarp = fsl.ApplyWarp(in_file=infile, ref_file=reffile, field_file=reffile, **{name: settings[1]})
    if name == 'out_file':
        realcmd = 'applywarp --in=%s --ref=%s --out=%s --warp=%s' % (infile, reffile, settings[1], reffile)
    else:
        outfile = awarp._gen_fname(infile, suffix='_warp')
        realcmd = 'applywarp --in=%s --ref=%s --out=%s --warp=%s %s' % (infile, reffile, outfile, reffile, settings[0])
    assert awarp.cmdline == realcmd
```

## Next Steps


---

*Source: test_preprocess.py:548 | Complexity: Intermediate | Last updated: 2026-05-18*