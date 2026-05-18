# How To: Use Syn Sdc

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test use syn sdc

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
# Fixtures: tmp_path, args, expectation
```

## Step-by-Step Guide

### Step 1: Assign bids_path = value

```python
bids_path = tmp_path / 'data'
```

**Verification:**
```python
assert opts.use_syn_sdc == expectation
```

### Step 2: Assign out_path = value

```python
out_path = tmp_path / 'out'
```

### Step 3: Assign args = value

```python
args = [str(bids_path), str(out_path), 'participant'] + args
```

### Step 4: Call bids_path.mkdir()

```python
bids_path.mkdir()
```

### Step 5: Assign parser = _build_parser(...)

```python
parser = _build_parser()
```

### Step 6: Assign cm = nullcontext(...)

```python
cm = nullcontext()
```

### Step 7: Call _reset_config()

```python
_reset_config()
```

### Step 8: Assign cm = pytest.raises(...)

```python
cm = pytest.raises(expectation)
```

### Step 9: Assign opts = parser.parse_args(...)

```python
opts = parser.parse_args(args)
```

**Verification:**
```python
assert opts.use_syn_sdc == expectation
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, args, expectation

# Workflow
bids_path = tmp_path / 'data'
out_path = tmp_path / 'out'
args = [str(bids_path), str(out_path), 'participant'] + args
bids_path.mkdir()
parser = _build_parser()
cm = nullcontext()
if isinstance(expectation, tuple):
    cm = pytest.raises(expectation)
with cm:
    opts = parser.parse_args(args)
if not isinstance(expectation, tuple):
    assert opts.use_syn_sdc == expectation
_reset_config()
```

## Next Steps


---

*Source: test_parser.py:212 | Complexity: Advanced | Last updated: 2026-05-18*