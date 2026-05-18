# How To: Frame Info

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: Test _frame_info.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `logging`
- `os`
- `re`
- `warnings`
- `pathlib`
- `numpy`
- `pytest`
- `mne`
- `mne.io`
- `mne.parallel`
- `mne.utils`
- `mne.utils._logging`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: capsys, monkeypatch
```

## Step-by-Step Guide

### Step 1: 'Test _frame_info.'

```python
'Test _frame_info.'
```

**Verification:**
```python
assert 2 < len(stack) < 100
```

### Step 2: Assign stack = _frame_info(...)

```python
stack = _frame_info(100)
```

**Verification:**
```python
assert re.match('^test_logging:[1-9][0-9]$', this) is not None, this
```

### Step 3: Assign unknown = value

```python
this, pytest_line = stack[:2]
```

**Verification:**
```python
assert 'pytest' in pytest_line
```

### Step 4: Call capsys.readouterr()

```python
capsys.readouterr()
```

**Verification:**
```python
assert re.match('.*pytest.*test_logging:[2-9][0-9] .*test_logging:[1-9][0-9] :.*Test', out) is not None, this
```

### Step 5: Assign unknown = capsys.readouterr(...)

```python
out, _ = capsys.readouterr()
```

**Verification:**
```python
assert _frame_info(1) == ['unknown']
```

### Step 6: Assign out = out.replace(...)

```python
out = out.replace('\n', ' ')
```

**Verification:**
```python
assert re.match('.*pytest.*test_logging:[2-9][0-9] .*test_logging:[1-9][0-9] :.*Test', out) is not None, this
```

### Step 7: Call monkeypatch.setattr()

```python
monkeypatch.setattr('inspect.currentframe', lambda: None)
```

**Verification:**
```python
assert _frame_info(1) == ['unknown']
```

### Step 8: Call _fun()

```python
_fun()
```


## Complete Example

```python
# Setup
# Fixtures: capsys, monkeypatch

# Workflow
'Test _frame_info.'
stack = _frame_info(100)
assert 2 < len(stack) < 100
this, pytest_line = stack[:2]
assert re.match('^test_logging:[1-9][0-9]$', this) is not None, this
assert 'pytest' in pytest_line
capsys.readouterr()
with use_log_level('debug', add_frames=4):
    _fun()
out, _ = capsys.readouterr()
out = out.replace('\n', ' ')
assert re.match('.*pytest.*test_logging:[2-9][0-9] .*test_logging:[1-9][0-9] :.*Test', out) is not None, this
monkeypatch.setattr('inspect.currentframe', lambda: None)
assert _frame_info(1) == ['unknown']
```

## Next Steps


---

*Source: test_logging.py:43 | Complexity: Advanced | Last updated: 2026-05-18*