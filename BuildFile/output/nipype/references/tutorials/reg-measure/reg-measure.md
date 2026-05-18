# How To: Reg Measure

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: tests for reg_measure interface

## Prerequisites

**Required Modules:**
- `os`
- `pytest`
- `utils.filemanip`
- `testing`


## Step-by-Step Guide

### Step 1: 'tests for reg_measure interface'

```python
'tests for reg_measure interface'
```

**Verification:**
```python
assert nr_measure.cmd == get_custom_path('reg_measure')
```

### Step 2: Assign nr_measure = RegMeasure(...)

```python
nr_measure = RegMeasure()
```

**Verification:**
```python
assert nr_measure.cmdline == expected_cmd
```

### Step 3: Assign ref_file = example_data(...)

```python
ref_file = example_data('im1.nii')
```

### Step 4: Assign flo_file = example_data(...)

```python
flo_file = example_data('im2.nii')
```

### Step 5: Assign nr_measure.inputs.ref_file = ref_file

```python
nr_measure.inputs.ref_file = ref_file
```

### Step 6: Assign nr_measure.inputs.flo_file = flo_file

```python
nr_measure.inputs.flo_file = flo_file
```

### Step 7: Assign nr_measure.inputs.measure_type = 'lncc'

```python
nr_measure.inputs.measure_type = 'lncc'
```

### Step 8: Assign nr_measure.inputs.omp_core_val = 4

```python
nr_measure.inputs.omp_core_val = 4
```

### Step 9: Assign cmd_tmp = '{cmd} -flo {flo} -lncc -omp 4 -out {out} -ref {ref}'

```python
cmd_tmp = '{cmd} -flo {flo} -lncc -omp 4 -out {out} -ref {ref}'
```

### Step 10: Assign expected_cmd = cmd_tmp.format(...)

```python
expected_cmd = cmd_tmp.format(cmd=get_custom_path('reg_measure'), flo=flo_file, out='im2_lncc.txt', ref=ref_file)
```

**Verification:**
```python
assert nr_measure.cmdline == expected_cmd
```

### Step 11: Call nr_measure.run()

```python
nr_measure.run()
```


## Complete Example

```python
# Workflow
'tests for reg_measure interface'
nr_measure = RegMeasure()
assert nr_measure.cmd == get_custom_path('reg_measure')
with pytest.raises(ValueError):
    nr_measure.run()
ref_file = example_data('im1.nii')
flo_file = example_data('im2.nii')
nr_measure.inputs.ref_file = ref_file
nr_measure.inputs.flo_file = flo_file
nr_measure.inputs.measure_type = 'lncc'
nr_measure.inputs.omp_core_val = 4
cmd_tmp = '{cmd} -flo {flo} -lncc -omp 4 -out {out} -ref {ref}'
expected_cmd = cmd_tmp.format(cmd=get_custom_path('reg_measure'), flo=flo_file, out='im2_lncc.txt', ref=ref_file)
assert nr_measure.cmdline == expected_cmd
```

## Next Steps


---

*Source: test_regutils.py:501 | Complexity: Advanced | Last updated: 2026-05-18*