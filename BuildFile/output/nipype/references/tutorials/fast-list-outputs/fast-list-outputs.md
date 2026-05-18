# How To: Fast List Outputs

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: By default (no -o), FSL's fast command outputs files into the same
directory as the input files. If the flag -o is set, it outputs files into
the cwd

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
# Fixtures: setup_infile, tmpdir
```

## Step-by-Step Guide

### Step 1: "By default (no -o), FSL's fast command outputs files into the same\n    directory as the input files. If the flag -o is set, it outputs files into\n    the cwd"

```python
"By default (no -o), FSL's fast command outputs files into the same\n    directory as the input files. If the flag -o is set, it outputs files into\n    the cwd"
```

**Verification:**
```python
assert os.path.realpath(filename).startswith(os.path.realpath(output_base))
```

### Step 2: Assign unknown = setup_infile

```python
tmp_infile, indir = setup_infile
```

**Verification:**
```python
assert indir != cwd.strpath
```

### Step 3: Assign cwd = tmpdir.mkdir(...)

```python
cwd = tmpdir.mkdir('new')
```

### Step 4: Call cwd.chdir()

```python
cwd.chdir()
```

**Verification:**
```python
assert indir != cwd.strpath
```

### Step 5: Assign out_basename = 'a_basename'

```python
out_basename = 'a_basename'
```

### Step 6: Assign opts = value

```python
opts = {'in_files': tmp_infile}
```

### Step 7: Assign unknown = split_filename(...)

```python
input_path, input_filename, input_ext = split_filename(tmp_infile)
```

### Step 8: Call _run_and_test()

```python
_run_and_test(opts, os.path.join(input_path, input_filename))
```

### Step 9: Assign unknown = out_basename

```python
opts['out_basename'] = out_basename
```

### Step 10: Call _run_and_test()

```python
_run_and_test(opts, os.path.join(cwd.strpath, out_basename))
```

### Step 11: Assign outputs = fsl.FAST._list_outputs(...)

```python
outputs = fsl.FAST(**opts)._list_outputs()
```

**Verification:**
```python
assert os.path.realpath(filename).startswith(os.path.realpath(output_base))
```


## Complete Example

```python
# Setup
# Fixtures: setup_infile, tmpdir

# Workflow
"By default (no -o), FSL's fast command outputs files into the same\n    directory as the input files. If the flag -o is set, it outputs files into\n    the cwd"

def _run_and_test(opts, output_base):
    outputs = fsl.FAST(**opts)._list_outputs()
    for output in outputs.values():
        if output:
            for filename in ensure_list(output):
                assert os.path.realpath(filename).startswith(os.path.realpath(output_base))
tmp_infile, indir = setup_infile
cwd = tmpdir.mkdir('new')
cwd.chdir()
assert indir != cwd.strpath
out_basename = 'a_basename'
opts = {'in_files': tmp_infile}
input_path, input_filename, input_ext = split_filename(tmp_infile)
_run_and_test(opts, os.path.join(input_path, input_filename))
opts['out_basename'] = out_basename
_run_and_test(opts, os.path.join(cwd.strpath, out_basename))
```

## Next Steps


---

*Source: test_preprocess.py:151 | Complexity: Advanced | Last updated: 2026-05-18*