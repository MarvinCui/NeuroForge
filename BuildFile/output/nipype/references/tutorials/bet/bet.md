# How To: Bet

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test bet

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
# Fixtures: setup_infile
```

## Step-by-Step Guide

### Step 1: Assign unknown = setup_infile

```python
tmp_infile, tp_dir = setup_infile
```

**Verification:**
```python
assert better.cmd == 'bet'
```

### Step 2: Assign tmp_infile = os.path.relpath(...)

```python
tmp_infile = os.path.relpath(tmp_infile, start=os.getcwd())
```

**Verification:**
```python
assert better.cmdline == realcmd
```

### Step 3: Assign better = fsl.BET(...)

```python
better = fsl.BET()
```

**Verification:**
```python
assert better.cmdline == realcmd
```

### Step 4: Assign better.inputs.in_file = tmp_infile

```python
better.inputs.in_file = tmp_infile
```

**Verification:**
```python
assert better.cmdline == realcmd
```

### Step 5: Assign outfile = fsl_name(...)

```python
outfile = fsl_name(better, 'foo_brain')
```

### Step 6: Assign realcmd = value

```python
realcmd = f'bet {tmp_infile} {outfile}'
```

**Verification:**
```python
assert better.cmdline == realcmd
```

### Step 7: Assign outfile = fsl_name(...)

```python
outfile = fsl_name(better, '/newdata/bar')
```

### Step 8: Assign better.inputs.out_file = outfile

```python
better.inputs.out_file = outfile
```

### Step 9: Assign realcmd = value

```python
realcmd = f'bet {tmp_infile} {outfile}'
```

**Verification:**
```python
assert better.cmdline == realcmd
```

### Step 10: Assign opt_map = value

```python
opt_map = {'outline': ('-o', True), 'mask': ('-m', True), 'skull': ('-s', True), 'no_output': ('-n', True), 'frac': ('-f 0.40', 0.4), 'vertical_gradient': ('-g 0.75', 0.75), 'radius': ('-r 20', 20), 'center': ('-c 54 75 80', [54, 75, 80]), 'threshold': ('-t', True), 'mesh': ('-e', True), 'surfaces': ('-A', True)}
```

### Step 11: Assign better = fsl.BET(...)

```python
better = fsl.BET()
```

### Step 12: Assign outfile = fsl_name(...)

```python
outfile = fsl_name(better, 'foo_brain')
```

### Step 13: Call better.run()

```python
better.run()
```

### Step 14: Call better.run()

```python
better.run(in_file='foo2.nii', out_file='bar.nii')
```

### Step 15: Call func()

```python
func()
```

### Step 16: Assign better = fsl.BET(...)

```python
better = fsl.BET(**{name: settings[1]})
```

### Step 17: Assign better.inputs.in_file = tmp_infile

```python
better.inputs.in_file = tmp_infile
```

### Step 18: Assign realcmd = unknown.join(...)

```python
realcmd = ' '.join([better.cmd, tmp_infile, outfile, settings[0]])
```

**Verification:**
```python
assert better.cmdline == realcmd
```


## Complete Example

```python
# Setup
# Fixtures: setup_infile

# Workflow
tmp_infile, tp_dir = setup_infile
tmp_infile = os.path.relpath(tmp_infile, start=os.getcwd())
better = fsl.BET()
assert better.cmd == 'bet'
with pytest.raises(ValueError):
    better.run()
better.inputs.in_file = tmp_infile
outfile = fsl_name(better, 'foo_brain')
realcmd = f'bet {tmp_infile} {outfile}'
assert better.cmdline == realcmd
outfile = fsl_name(better, '/newdata/bar')
better.inputs.out_file = outfile
realcmd = f'bet {tmp_infile} {outfile}'
assert better.cmdline == realcmd

def func():
    better.run(in_file='foo2.nii', out_file='bar.nii')
with pytest.raises(TraitError):
    func()
opt_map = {'outline': ('-o', True), 'mask': ('-m', True), 'skull': ('-s', True), 'no_output': ('-n', True), 'frac': ('-f 0.40', 0.4), 'vertical_gradient': ('-g 0.75', 0.75), 'radius': ('-r 20', 20), 'center': ('-c 54 75 80', [54, 75, 80]), 'threshold': ('-t', True), 'mesh': ('-e', True), 'surfaces': ('-A', True)}
better = fsl.BET()
outfile = fsl_name(better, 'foo_brain')
for name, settings in list(opt_map.items()):
    better = fsl.BET(**{name: settings[1]})
    better.inputs.in_file = tmp_infile
    realcmd = ' '.join([better.cmd, tmp_infile, outfile, settings[0]])
    assert better.cmdline == realcmd
```

## Next Steps


---

*Source: test_preprocess.py:29 | Complexity: Advanced | Last updated: 2026-05-18*