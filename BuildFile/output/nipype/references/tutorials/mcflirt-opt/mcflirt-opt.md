# How To: Mcflirt Opt

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test mcflirt opt

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
assert fnt.cmdline == ' '.join([fnt.cmd, instr, settings[0], outstr])
```

### Step 2: Assign unknown = os.path.split(...)

```python
_, nme = os.path.split(infile)
```

**Verification:**
```python
assert fnt.cmdline == ' '.join([fnt.cmd, instr, outstr, settings[0]])
```

### Step 3: Assign opt_map = value

```python
opt_map = {'cost': ('-cost mutualinfo', 'mutualinfo'), 'bins': ('-bins 256', 256), 'dof': ('-dof 6', 6), 'ref_vol': ('-refvol 2', 2), 'scaling': ('-scaling 6.00', 6.0), 'smooth': ('-smooth 1.00', 1.0), 'rotation': ('-rotation 2', 2), 'stages': ('-stages 3', 3), 'init': ('-init %s' % infile, infile), 'use_gradient': ('-gdt', True), 'use_contour': ('-edge', True), 'mean_vol': ('-meanvol', True), 'stats_imgs': ('-stats', True), 'save_mats': ('-mats', True), 'save_plots': ('-plots', True)}
```

### Step 4: Assign fnt = fsl.MCFLIRT(...)

```python
fnt = fsl.MCFLIRT(in_file=infile, **{name: settings[1]})
```

### Step 5: Assign outfile = os.path.join(...)

```python
outfile = os.path.join(os.getcwd(), nme)
```

### Step 6: Assign outfile = fnt._gen_fname(...)

```python
outfile = fnt._gen_fname(outfile, suffix='_mcf')
```

### Step 7: Assign instr = value

```python
instr = '-in %s' % infile
```

### Step 8: Assign outstr = value

```python
outstr = '-out %s' % outfile
```

**Verification:**
```python
assert fnt.cmdline == ' '.join([fnt.cmd, instr, settings[0], outstr])
```


## Complete Example

```python
# Setup
# Fixtures: setup_flirt

# Workflow
tmpdir, infile, reffile = setup_flirt
_, nme = os.path.split(infile)
opt_map = {'cost': ('-cost mutualinfo', 'mutualinfo'), 'bins': ('-bins 256', 256), 'dof': ('-dof 6', 6), 'ref_vol': ('-refvol 2', 2), 'scaling': ('-scaling 6.00', 6.0), 'smooth': ('-smooth 1.00', 1.0), 'rotation': ('-rotation 2', 2), 'stages': ('-stages 3', 3), 'init': ('-init %s' % infile, infile), 'use_gradient': ('-gdt', True), 'use_contour': ('-edge', True), 'mean_vol': ('-meanvol', True), 'stats_imgs': ('-stats', True), 'save_mats': ('-mats', True), 'save_plots': ('-plots', True)}
for name, settings in list(opt_map.items()):
    fnt = fsl.MCFLIRT(in_file=infile, **{name: settings[1]})
    outfile = os.path.join(os.getcwd(), nme)
    outfile = fnt._gen_fname(outfile, suffix='_mcf')
    instr = '-in %s' % infile
    outstr = '-out %s' % outfile
    if name in ('init', 'cost', 'dof', 'mean_vol', 'bins'):
        assert fnt.cmdline == ' '.join([fnt.cmd, instr, settings[0], outstr])
    else:
        assert fnt.cmdline == ' '.join([fnt.cmd, instr, outstr, settings[0]])
```

## Next Steps


---

*Source: test_preprocess.py:354 | Complexity: Advanced | Last updated: 2026-05-18*