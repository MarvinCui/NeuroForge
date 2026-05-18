# How To: Plottimeseries

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test plottimeseries

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
assert plotter.cmdline == "fsl_tsplot -i %s -a x,y,z -o foo.png -t 'test plot' -u 1 --ymin=0 --ymax=1" % parfiles[0]
```

### Step 3: Assign plotter = fsl.PlotTimeSeries(...)

```python
plotter = fsl.PlotTimeSeries()
```

**Verification:**
```python
assert plotter2.cmdline == "fsl_tsplot -i %s,%s -o bar.png --start=2 --finish=5 -t 'test2 plot' -u 1" % tuple(parfiles)
```

### Step 4: Assign plotter.inputs.in_file = value

```python
plotter.inputs.in_file = parfiles[0]
```

### Step 5: Assign plotter.inputs.labels = value

```python
plotter.inputs.labels = ['x', 'y', 'z']
```

### Step 6: Assign plotter.inputs.y_range = value

```python
plotter.inputs.y_range = (0, 1)
```

### Step 7: Assign plotter.inputs.title = 'test plot'

```python
plotter.inputs.title = 'test plot'
```

### Step 8: Assign plotter.inputs.out_file = 'foo.png'

```python
plotter.inputs.out_file = 'foo.png'
```

**Verification:**
```python
assert plotter.cmdline == "fsl_tsplot -i %s -a x,y,z -o foo.png -t 'test plot' -u 1 --ymin=0 --ymax=1" % parfiles[0]
```

### Step 9: Assign plotter2 = fsl.PlotTimeSeries(...)

```python
plotter2 = fsl.PlotTimeSeries(in_file=parfiles, title='test2 plot', plot_range=(2, 5), out_file='bar.png')
```

**Verification:**
```python
assert plotter2.cmdline == "fsl_tsplot -i %s,%s -o bar.png --start=2 --finish=5 -t 'test2 plot' -u 1" % tuple(parfiles)
```

### Step 10: Call plotter.run()

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
plotter = fsl.PlotTimeSeries()
assert plotter.cmd == 'fsl_tsplot'
with pytest.raises(ValueError):
    plotter.run()
plotter.inputs.in_file = parfiles[0]
plotter.inputs.labels = ['x', 'y', 'z']
plotter.inputs.y_range = (0, 1)
plotter.inputs.title = 'test plot'
plotter.inputs.out_file = 'foo.png'
assert plotter.cmdline == "fsl_tsplot -i %s -a x,y,z -o foo.png -t 'test plot' -u 1 --ymin=0 --ymax=1" % parfiles[0]
plotter2 = fsl.PlotTimeSeries(in_file=parfiles, title='test2 plot', plot_range=(2, 5), out_file='bar.png')
assert plotter2.cmdline == "fsl_tsplot -i %s,%s -o bar.png --start=2 --finish=5 -t 'test2 plot' -u 1" % tuple(parfiles)
```

## Next Steps


---

*Source: test_utils.py:228 | Complexity: Advanced | Last updated: 2026-05-18*