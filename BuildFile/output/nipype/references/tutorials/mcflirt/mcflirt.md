# How To: Mcflirt

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test mcflirt

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
assert frt.cmd == 'mcflirt'
```

### Step 2: Assign frt = fsl.MCFLIRT(...)

```python
frt = fsl.MCFLIRT()
```

**Verification:**
```python
assert frt.cmdline == realcmd
```

### Step 3: Assign frt.inputs.in_file = infile

```python
frt.inputs.in_file = infile
```

**Verification:**
```python
assert frt.cmdline == realcmd
```

### Step 4: Assign unknown = os.path.split(...)

```python
_, nme = os.path.split(infile)
```

### Step 5: Assign outfile = os.path.join(...)

```python
outfile = os.path.join(os.getcwd(), nme)
```

### Step 6: Assign outfile = frt._gen_fname(...)

```python
outfile = frt._gen_fname(outfile, suffix='_mcf')
```

### Step 7: Assign realcmd = value

```python
realcmd = 'mcflirt -in ' + infile + ' -out ' + outfile
```

**Verification:**
```python
assert frt.cmdline == realcmd
```

### Step 8: Assign outfile2 = '/newdata/bar.nii'

```python
outfile2 = '/newdata/bar.nii'
```

### Step 9: Assign frt.inputs.out_file = outfile2

```python
frt.inputs.out_file = outfile2
```

### Step 10: Assign realcmd = value

```python
realcmd = 'mcflirt -in ' + infile + ' -out ' + outfile2
```

**Verification:**
```python
assert frt.cmdline == realcmd
```


## Complete Example

```python
# Setup
# Fixtures: setup_flirt

# Workflow
tmpdir, infile, reffile = setup_flirt
frt = fsl.MCFLIRT()
assert frt.cmd == 'mcflirt'
frt.inputs.in_file = infile
_, nme = os.path.split(infile)
outfile = os.path.join(os.getcwd(), nme)
outfile = frt._gen_fname(outfile, suffix='_mcf')
realcmd = 'mcflirt -in ' + infile + ' -out ' + outfile
assert frt.cmdline == realcmd
outfile2 = '/newdata/bar.nii'
frt.inputs.out_file = outfile2
realcmd = 'mcflirt -in ' + infile + ' -out ' + outfile2
assert frt.cmdline == realcmd
```

## Next Steps


---

*Source: test_preprocess.py:333 | Complexity: Advanced | Last updated: 2026-05-18*