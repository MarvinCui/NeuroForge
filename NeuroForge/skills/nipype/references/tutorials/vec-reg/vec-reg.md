# How To: Vec Reg

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test Vec reg

## Prerequisites

**Required Modules:**
- `os`
- `nipype.interfaces.fsl.dti`
- `nipype.interfaces.fsl`
- `nipype.interfaces.base`
- `pytest`
- `nipype.testing.fixtures`


## Step-by-Step Guide

### Step 1: Assign vrg = fsl.VecReg(...)

```python
vrg = fsl.VecReg()
```

**Verification:**
```python
assert vrg.cmd == 'vecreg'
```

### Step 2: Assign vrg.inputs.infile = 'infile'

```python
vrg.inputs.infile = 'infile'
```

**Verification:**
```python
assert vrg.cmdline == 'vecreg -i infile -o outfile -r MNI152 -t tmat.mat'
```

### Step 3: Assign vrg.inputs.outfile = 'outfile'

```python
vrg.inputs.outfile = 'outfile'
```

**Verification:**
```python
assert actualCmdline == desiredCmdline
```

### Step 4: Assign vrg.inputs.refVolName = 'MNI152'

```python
vrg.inputs.refVolName = 'MNI152'
```

**Verification:**
```python
assert results.runtime.cmdline == 'vecreg -i infile3 -o outfile3 -r MNI152 -t tmat3.mat'
```

### Step 5: Assign vrg.inputs.affineTmat = 'tmat.mat'

```python
vrg.inputs.affineTmat = 'tmat.mat'
```

**Verification:**
```python
assert results.runtime.returncode != 0
```

### Step 6: Assign vrg2 = fsl.VecReg(...)

```python
vrg2 = fsl.VecReg(infile='infile2', outfile='outfile2', refVolName='MNI152', affineTmat='tmat2.mat', brainMask='nodif_brain_mask')
```

**Verification:**
```python
assert results.interface.inputs.infile == 'infile3'
```

### Step 7: Assign actualCmdline = sorted(...)

```python
actualCmdline = sorted(vrg2.cmdline.split())
```

**Verification:**
```python
assert results.interface.inputs.outfile == 'outfile3'
```

### Step 8: Assign cmd = 'vecreg -i infile2 -o outfile2 -r MNI152 -t tmat2.mat -m nodif_brain_mask'

```python
cmd = 'vecreg -i infile2 -o outfile2 -r MNI152 -t tmat2.mat -m nodif_brain_mask'
```

**Verification:**
```python
assert results.interface.inputs.refVolName == 'MNI152'
```

### Step 9: Assign desiredCmdline = sorted(...)

```python
desiredCmdline = sorted(cmd.split())
```

**Verification:**
```python
assert results.interface.inputs.affineTmat == 'tmat3.mat'
```

### Step 10: Assign vrg3 = fsl.VecReg(...)

```python
vrg3 = fsl.VecReg()
```

**Verification:**
```python
assert vrg4.cmdline == vrg4.cmd + ' -i infile -o outfile -r MNI152 ' + settings[0]
```

### Step 11: Assign results = vrg3.run(...)

```python
results = vrg3.run(infile='infile3', outfile='outfile3', refVolName='MNI152', affineTmat='tmat3.mat')
```

**Verification:**
```python
assert results.runtime.cmdline == 'vecreg -i infile3 -o outfile3 -r MNI152 -t tmat3.mat'
```

### Step 12: Assign opt_map = value

```python
opt_map = {'verbose': ('-v', True), 'helpDoc': ('-h', True), 'tensor': ('--tensor', True), 'affineTmat': ('-t Tmat', 'Tmat'), 'warpFile': ('-w wrpFile', 'wrpFile'), 'interpolation': ('--interp=sinc', 'sinc'), 'brainMask': ('-m mask', 'mask')}
```

### Step 13: Call vrg.run()

```python
vrg.run()
```

### Step 14: Assign vrg4 = fsl.VecReg(...)

```python
vrg4 = fsl.VecReg(infile='infile', outfile='outfile', refVolName='MNI152', **{name: settings[1]})
```

**Verification:**
```python
assert vrg4.cmdline == vrg4.cmd + ' -i infile -o outfile -r MNI152 ' + settings[0]
```


## Complete Example

```python
# Workflow
vrg = fsl.VecReg()
assert vrg.cmd == 'vecreg'
with pytest.raises(ValueError):
    vrg.run()
vrg.inputs.infile = 'infile'
vrg.inputs.outfile = 'outfile'
vrg.inputs.refVolName = 'MNI152'
vrg.inputs.affineTmat = 'tmat.mat'
assert vrg.cmdline == 'vecreg -i infile -o outfile -r MNI152 -t tmat.mat'
vrg2 = fsl.VecReg(infile='infile2', outfile='outfile2', refVolName='MNI152', affineTmat='tmat2.mat', brainMask='nodif_brain_mask')
actualCmdline = sorted(vrg2.cmdline.split())
cmd = 'vecreg -i infile2 -o outfile2 -r MNI152 -t tmat2.mat -m nodif_brain_mask'
desiredCmdline = sorted(cmd.split())
assert actualCmdline == desiredCmdline
vrg3 = fsl.VecReg()
results = vrg3.run(infile='infile3', outfile='outfile3', refVolName='MNI152', affineTmat='tmat3.mat')
assert results.runtime.cmdline == 'vecreg -i infile3 -o outfile3 -r MNI152 -t tmat3.mat'
assert results.runtime.returncode != 0
assert results.interface.inputs.infile == 'infile3'
assert results.interface.inputs.outfile == 'outfile3'
assert results.interface.inputs.refVolName == 'MNI152'
assert results.interface.inputs.affineTmat == 'tmat3.mat'
opt_map = {'verbose': ('-v', True), 'helpDoc': ('-h', True), 'tensor': ('--tensor', True), 'affineTmat': ('-t Tmat', 'Tmat'), 'warpFile': ('-w wrpFile', 'wrpFile'), 'interpolation': ('--interp=sinc', 'sinc'), 'brainMask': ('-m mask', 'mask')}
for name, settings in list(opt_map.items()):
    vrg4 = fsl.VecReg(infile='infile', outfile='outfile', refVolName='MNI152', **{name: settings[1]})
    assert vrg4.cmdline == vrg4.cmd + ' -i infile -o outfile -r MNI152 ' + settings[0]
```

## Next Steps


---

*Source: test_dti.py:233 | Complexity: Advanced | Last updated: 2026-05-18*