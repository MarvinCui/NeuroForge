# How To: Bids Filter File

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test bids filter file

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
# Fixtures: tmp_path, capsys
```

## Step-by-Step Guide

### Step 1: Assign bids_path = value

```python
bids_path = tmp_path / 'data'
```

**Verification:**
```python
assert 'Path does not exist:' in err
```

### Step 2: Assign out_path = value

```python
out_path = tmp_path / 'out'
```

**Verification:**
```python
assert 'JSON syntax error in:' in err
```

### Step 3: Assign bff = value

```python
bff = tmp_path / 'filter.json'
```

### Step 4: Assign args = value

```python
args = [str(bids_path), str(out_path), 'participant', '--bids-filter-file', str(bff)]
```

### Step 5: Call bids_path.mkdir()

```python
bids_path.mkdir()
```

### Step 6: Assign parser = _build_parser(...)

```python
parser = _build_parser()
```

### Step 7: Assign err = value

```python
err = capsys.readouterr().err
```

**Verification:**
```python
assert 'Path does not exist:' in err
```

### Step 8: Call bff.write_text()

```python
bff.write_text('{"invalid json": }')
```

### Step 9: Assign err = value

```python
err = capsys.readouterr().err
```

**Verification:**
```python
assert 'JSON syntax error in:' in err
```

### Step 10: Call _reset_config()

```python
_reset_config()
```

### Step 11: Call parser.parse_args()

```python
parser.parse_args(args)
```

### Step 12: Call parser.parse_args()

```python
parser.parse_args(args)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, capsys

# Workflow
bids_path = tmp_path / 'data'
out_path = tmp_path / 'out'
bff = tmp_path / 'filter.json'
args = [str(bids_path), str(out_path), 'participant', '--bids-filter-file', str(bff)]
bids_path.mkdir()
parser = _build_parser()
with pytest.raises(SystemExit):
    parser.parse_args(args)
err = capsys.readouterr().err
assert 'Path does not exist:' in err
bff.write_text('{"invalid json": }')
with pytest.raises(SystemExit):
    parser.parse_args(args)
err = capsys.readouterr().err
assert 'JSON syntax error in:' in err
_reset_config()
```

## Next Steps


---

*Source: test_parser.py:162 | Complexity: Advanced | Last updated: 2026-05-18*