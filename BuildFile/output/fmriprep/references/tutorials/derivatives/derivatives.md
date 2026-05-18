# How To: Derivatives

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Check the correct parsing of the derivatives argument.

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
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Check the correct parsing of the derivatives argument.'

```python
'Check the correct parsing of the derivatives argument.'
```

**Verification:**
```python
assert opts.derivatives == {'smriprep': bids_path / 'derivatives/smriprep'}
```

### Step 2: Assign bids_path = value

```python
bids_path = tmp_path / 'data'
```

**Verification:**
```python
assert opts.derivatives == {'anat': bids_path / 'derivatives/smriprep'}
```

### Step 3: Assign out_path = value

```python
out_path = tmp_path / 'out'
```

### Step 4: Assign args = value

```python
args = [str(bids_path), str(out_path), 'participant']
```

### Step 5: Call bids_path.mkdir()

```python
bids_path.mkdir()
```

### Step 6: Assign parser = _build_parser(...)

```python
parser = _build_parser()
```

### Step 7: Assign temp_args = value

```python
temp_args = args + ['--derivatives']
```

### Step 8: Call _reset_config()

```python
_reset_config()
```

### Step 9: Assign temp_args = value

```python
temp_args = args + ['--derivatives', str(bids_path / 'derivatives/smriprep')]
```

### Step 10: Assign opts = parser.parse_args(...)

```python
opts = parser.parse_args(temp_args)
```

**Verification:**
```python
assert opts.derivatives == {'smriprep': bids_path / 'derivatives/smriprep'}
```

### Step 11: Call _reset_config()

```python
_reset_config()
```

### Step 12: Assign temp_args = value

```python
temp_args = args + ['--derivatives', f"anat={bids_path / 'derivatives/smriprep'}"]
```

### Step 13: Assign opts = parser.parse_args(...)

```python
opts = parser.parse_args(temp_args)
```

**Verification:**
```python
assert opts.derivatives == {'anat': bids_path / 'derivatives/smriprep'}
```

### Step 14: Call _reset_config()

```python
_reset_config()
```

### Step 15: Assign temp_args = value

```python
temp_args = args + ['--derivatives', str(bids_path / 'derivatives_01/smriprep'), str(bids_path / 'derivatives_02/smriprep')]
```

### Step 16: Call _reset_config()

```python
_reset_config()
```

### Step 17: Call parser.parse_args()

```python
parser.parse_args(temp_args)
```

### Step 18: Call parser.parse_args()

```python
parser.parse_args(temp_args)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Check the correct parsing of the derivatives argument.'
bids_path = tmp_path / 'data'
out_path = tmp_path / 'out'
args = [str(bids_path), str(out_path), 'participant']
bids_path.mkdir()
parser = _build_parser()
temp_args = args + ['--derivatives']
with pytest.raises((SystemExit, ArgumentError)):
    parser.parse_args(temp_args)
_reset_config()
temp_args = args + ['--derivatives', str(bids_path / 'derivatives/smriprep')]
opts = parser.parse_args(temp_args)
assert opts.derivatives == {'smriprep': bids_path / 'derivatives/smriprep'}
_reset_config()
temp_args = args + ['--derivatives', f"anat={bids_path / 'derivatives/smriprep'}"]
opts = parser.parse_args(temp_args)
assert opts.derivatives == {'anat': bids_path / 'derivatives/smriprep'}
_reset_config()
temp_args = args + ['--derivatives', str(bids_path / 'derivatives_01/smriprep'), str(bids_path / 'derivatives_02/smriprep')]
with pytest.raises(ValueError, match='Received duplicate derivative name'):
    parser.parse_args(temp_args)
_reset_config()
```

## Next Steps


---

*Source: test_parser.py:233 | Complexity: Advanced | Last updated: 2026-05-18*