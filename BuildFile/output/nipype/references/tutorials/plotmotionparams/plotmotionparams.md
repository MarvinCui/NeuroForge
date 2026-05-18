# How To: Plotmotionparams

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test plotmotionparams

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `numpy`
- `pytest`
- `nipype.interfaces.fsl.utils`
- `nipype.interfaces.fsl`
- `nipype.testing.fixtures`

**Setup Required:**
```python
# Fixtures: create_files_in_directory_plus_output_type
```

## Step-by-Step Guide

### Step 1: Assign unknown = create_files_in_directory_plus_output_type

```python
filelist, outdir, _ = create_files_in_directory_plus_output_type
```

**Verification:**
```python
assert plotter.cmd == 'fsl_tsplot'
```

### Step 2: Assign parfiles = create_parfiles(...)

```python
parfiles = create_parfiles()
```

**Verification:**
```python
assert plotter.cmdline == "fsl_tsplot -i %s -o foo.png -t 'MCFLIRT estimated rotations (radians)' --start=1 --finish=3 -a x,y,z" % parfiles[0]
```

### Step 3: Assign plotter = fsl.PlotMotionParams(...)

```python
plotter = fsl.PlotMotionParams()
```

**Verification:**
```python
assert plotter2.cmdline == "fsl_tsplot -i %s -o bar.png -t 'Realign estimated translations (mm)' --start=1 --finish=3 -a x,y,z" % parfiles[1]
```

### Step 4: Assign plotter.inputs.in_file = value

```python
plotter.inputs.in_file = parfiles[0]
```

### Step 5: Assign plotter.inputs.in_source = 'fsl'

```python
plotter.inputs.in_source = 'fsl'
```

### Step 6: Assign plotter.inputs.plot_type = 'rotations'

```python
plotter.inputs.plot_type = 'rotations'
```

### Step 7: Assign plotter.inputs.out_file = 'foo.png'

```python
plotter.inputs.out_file = 'foo.png'
```

**Verification:**
```python
assert plotter.cmdline == "fsl_tsplot -i %s -o foo.png -t 'MCFLIRT estimated rotations (radians)' --start=1 --finish=3 -a x,y,z" % parfiles[0]
```

### Step 8: Assign plotter2 = fsl.PlotMotionParams(...)

```python
plotter2 = fsl.PlotMotionParams(in_file=parfiles[1], in_source='spm', plot_type='translations', out_file='bar.png')
```

**Verification:**
```python
assert plotter2.cmdline == "fsl_tsplot -i %s -o bar.png -t 'Realign estimated translations (mm)' --start=1 --finish=3 -a x,y,z" % parfiles[1]
```

### Step 9: Call plotter.run()

```python
plotter.run()
```


## Complete Example

```python
# Setup
# Fixtures: create_files_in_directory_plus_output_type

# Workflow
filelist, outdir, _ = create_files_in_directory_plus_output_type
parfiles = create_parfiles()
plotter = fsl.PlotMotionParams()
assert plotter.cmd == 'fsl_tsplot'
with pytest.raises(ValueError):
    plotter.run()
plotter.inputs.in_file = parfiles[0]
plotter.inputs.in_source = 'fsl'
plotter.inputs.plot_type = 'rotations'
plotter.inputs.out_file = 'foo.png'
assert plotter.cmdline == "fsl_tsplot -i %s -o foo.png -t 'MCFLIRT estimated rotations (radians)' --start=1 --finish=3 -a x,y,z" % parfiles[0]
plotter2 = fsl.PlotMotionParams(in_file=parfiles[1], in_source='spm', plot_type='translations', out_file='bar.png')
assert plotter2.cmdline == "fsl_tsplot -i %s -o bar.png -t 'Realign estimated translations (mm)' --start=1 --finish=3 -a x,y,z" % parfiles[1]
```

## Next Steps


---

*Source: test_utils.py:263 | Complexity: Advanced | Last updated: 2026-05-18*