# How To: Memory Arg

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Check the correct parsing of the memory argument.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `argparse`
- `contextlib`
- `pytest`
- `packaging.version`
- `tests.test_config`
- `parser`
- `niworkflows.utils.testing`

**Setup Required:**
```python
# Fixtures: tmp_path, argval, gb
```

## Step-by-Step Guide

### Step 1: 'Check the correct parsing of the memory argument.'

```python
'Check the correct parsing of the memory argument.'
```

**Verification:**
```python
assert opts.memory_gb == gb
```

### Step 2: Assign datapath = value

```python
datapath = tmp_path / 'data'
```

### Step 3: Call datapath.mkdir()

```python
datapath.mkdir(exist_ok=True)
```

### Step 4: Assign _fs_file = value

```python
_fs_file = tmp_path / 'license.txt'
```

### Step 5: Call _fs_file.write_text()

```python
_fs_file.write_text('')
```

### Step 6: Assign args = value

```python
args = [str(datapath)] + MIN_ARGS[1:] + ['--fs-license-file', str(_fs_file), '--mem', argval]
```

### Step 7: Assign opts = _build_parser.parse_args(...)

```python
opts = _build_parser().parse_args(args)
```

**Verification:**
```python
assert opts.memory_gb == gb
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, argval, gb

# Workflow
'Check the correct parsing of the memory argument.'
datapath = tmp_path / 'data'
datapath.mkdir(exist_ok=True)
_fs_file = tmp_path / 'license.txt'
_fs_file.write_text('')
args = [str(datapath)] + MIN_ARGS[1:] + ['--fs-license-file', str(_fs_file), '--mem', argval]
opts = _build_parser().parse_args(args)
assert opts.memory_gb == gb
```

## Next Steps


---

*Source: test_parser.py:90 | Complexity: Intermediate | Last updated: 2026-05-18*