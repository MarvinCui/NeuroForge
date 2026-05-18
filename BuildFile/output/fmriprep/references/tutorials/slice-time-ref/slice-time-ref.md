# How To: Slice Time Ref

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test slice time ref

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
# Fixtures: tmp_path, st_ref
```

## Step-by-Step Guide

### Step 1: Assign bids_path = value

```python
bids_path = tmp_path / 'data'
```

### Step 2: Assign out_path = value

```python
out_path = tmp_path / 'out'
```

### Step 3: Assign args = value

```python
args = [str(bids_path), str(out_path), 'participant']
```

### Step 4: Call bids_path.mkdir()

```python
bids_path.mkdir()
```

### Step 5: Assign parser = _build_parser(...)

```python
parser = _build_parser()
```

### Step 6: Call parser.parse_args()

```python
parser.parse_args(args)
```

### Step 7: Call _reset_config()

```python
_reset_config()
```

### Step 8: Call args.extend()

```python
args.extend(['--slice-time-ref', st_ref])
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, st_ref

# Workflow
bids_path = tmp_path / 'data'
out_path = tmp_path / 'out'
args = [str(bids_path), str(out_path), 'participant']
if st_ref:
    args.extend(['--slice-time-ref', st_ref])
bids_path.mkdir()
parser = _build_parser()
parser.parse_args(args)
_reset_config()
```

## Next Steps


---

*Source: test_parser.py:188 | Complexity: Advanced | Last updated: 2026-05-18*