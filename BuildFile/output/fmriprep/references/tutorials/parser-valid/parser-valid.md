# How To: Parser Valid

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Check valid arguments.

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
# Fixtures: tmp_path, args
```

## Step-by-Step Guide

### Step 1: 'Check valid arguments.'

```python
'Check valid arguments.'
```

**Verification:**
```python
assert opts.bids_dir == datapath
```

### Step 2: Assign datapath = value

```python
datapath = tmp_path / 'data'
```

### Step 3: Call datapath.mkdir()

```python
datapath.mkdir(exist_ok=True)
```

### Step 4: Assign unknown = str(...)

```python
args[0] = str(datapath)
```

### Step 5: Assign opts = _build_parser.parse_args(...)

```python
opts = _build_parser().parse_args(args)
```

**Verification:**
```python
assert opts.bids_dir == datapath
```

### Step 6: Assign _fs_file = value

```python
_fs_file = tmp_path / 'license.txt'
```

### Step 7: Call _fs_file.write_text()

```python
_fs_file.write_text('')
```

### Step 8: Call args.insert()

```python
args.insert(args.index('--fs-license-file') + 1, str(_fs_file.absolute()))
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, args

# Workflow
'Check valid arguments.'
datapath = tmp_path / 'data'
datapath.mkdir(exist_ok=True)
args[0] = str(datapath)
if '--fs-license-file' in args:
    _fs_file = tmp_path / 'license.txt'
    _fs_file.write_text('')
    args.insert(args.index('--fs-license-file') + 1, str(_fs_file.absolute()))
opts = _build_parser().parse_args(args)
assert opts.bids_dir == datapath
```

## Next Steps


---

*Source: test_parser.py:57 | Complexity: Advanced | Last updated: 2026-05-18*