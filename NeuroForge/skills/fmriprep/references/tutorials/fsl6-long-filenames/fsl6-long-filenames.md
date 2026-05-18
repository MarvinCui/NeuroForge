# How To: Fsl6 Long Filenames

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test fsl6 long filenames

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `shutil`
- `pathlib`
- `pytest`
- `templateflow.api`
- `looseversion`
- `nipype.interfaces`

**Setup Required:**
```python
# Fixtures: tmp_path, path_parent, filename
```

## Step-by-Step Guide

### Step 1: Assign test_dir = value

```python
test_dir = tmp_path / path_parent
```

**Verification:**
```python
assert Path(bet.outputs.out_file).exists()
```

### Step 2: Call test_dir.mkdir()

```python
test_dir.mkdir(parents=True, exist_ok=True)
```

### Step 3: Assign in_file = value

```python
in_file = test_dir / filename
```

### Step 4: Assign out_file = value

```python
out_file = test_dir / 'output.nii.gz'
```

### Step 5: Call shutil.copy()

```python
shutil.copy(TEMPLATE, in_file)
```

### Step 6: Assign bet = fsl.BET.run(...)

```python
bet = fsl.BET(in_file=in_file, out_file=out_file).run()
```

**Verification:**
```python
assert Path(bet.outputs.out_file).exists()
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, path_parent, filename

# Workflow
test_dir = tmp_path / path_parent
test_dir.mkdir(parents=True, exist_ok=True)
in_file = test_dir / filename
out_file = test_dir / 'output.nii.gz'
shutil.copy(TEMPLATE, in_file)
bet = fsl.BET(in_file=in_file, out_file=out_file).run()
assert Path(bet.outputs.out_file).exists()
```

## Next Steps


---

*Source: test_fsl6.py:32 | Complexity: Intermediate | Last updated: 2026-05-18*