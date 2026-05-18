# How To: Sys Info Check Outdated

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: mock, pytest, workflow, integration

## Overview

Workflow: Test sys info checking.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `json`
- `os`
- `platform`
- `random`
- `re`
- `time`
- `functools`
- `pathlib`
- `urllib.error`
- `pytest`
- `mne`
- `mne.utils.config`
- `mne.utils`
- `joblib`

**Setup Required:**
```python
# Fixtures: monkeypatch
```

## Step-by-Step Guide

### Step 1: 'Test sys info checking.'

```python
'Test sys info checking.'
```

**Verification:**
```python
assert '(outdated, release ' in out
```

### Step 2: Call monkeypatch.setattr()

```python
monkeypatch.setattr(mne, '__version__', '0.1')
```

**Verification:**
```python
assert 'updating.html' in out
```

### Step 3: Assign out = ClosingStringIO(...)

```python
out = ClosingStringIO()
```

**Verification:**
```python
assert re.match('.*unable to check.*timeout.*', out, re.DOTALL) is not None
```

### Step 4: Call sys_info()

```python
sys_info(fid=out, check_version=10)
```

**Verification:**
```python
assert 'updating.html' not in out
```

### Step 5: Assign out = out.getvalue(...)

```python
out = out.getvalue()
```

**Verification:**
```python
assert '(outdated, release ' in out
```

### Step 6: Assign out = ClosingStringIO(...)

```python
out = ClosingStringIO()
```

### Step 7: Call sys_info()

```python
sys_info(fid=out, check_version=1e-12)
```

### Step 8: Assign out = out.getvalue(...)

```python
out = out.getvalue()
```

**Verification:**
```python
assert re.match('.*unable to check.*timeout.*', out, re.DOTALL) is not None
```


## Complete Example

```python
# Setup
# Fixtures: monkeypatch

# Workflow
'Test sys info checking.'
monkeypatch.setattr(mne, '__version__', '0.1')
out = ClosingStringIO()
sys_info(fid=out, check_version=10)
out = out.getvalue()
assert '(outdated, release ' in out
assert 'updating.html' in out
out = ClosingStringIO()
sys_info(fid=out, check_version=1e-12)
out = out.getvalue()
assert re.match('.*unable to check.*timeout.*', out, re.DOTALL) is not None
assert 'updating.html' not in out
```

## Next Steps


---

*Source: test_config.py:184 | Complexity: Advanced | Last updated: 2026-05-18*