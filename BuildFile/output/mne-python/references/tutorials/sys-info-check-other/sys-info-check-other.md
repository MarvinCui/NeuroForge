# How To: Sys Info Check Other

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: Test other failure modes of the sys info check.

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

### Step 1: 'Test other failure modes of the sys info check.'

```python
'Test other failure modes of the sys info check.'
```

**Verification:**
```python
assert re.match('.*unable to check.*SSL.*', out, re.DOTALL) is not None
```

### Step 2: Assign out = ClosingStringIO(...)

```python
out = ClosingStringIO()
```

**Verification:**
```python
assert match is not None
```

### Step 3: Assign out = out.getvalue(...)

```python
out = out.getvalue()
```

**Verification:**
```python
assert ' 1.5.1 (latest release)' in out
```

### Step 4: Assign out = ClosingStringIO(...)

```python
out = ClosingStringIO()
```

**Verification:**
```python
assert 'development, ' in out
```

### Step 5: Assign out = out.getvalue(...)

```python
out = out.getvalue()
```

**Verification:**
```python
assert 'updating.html' not in out
```

### Step 6: Assign match = re.match(...)

```python
match = re.match('.*unable to .*unknown error: .*foo bar.*', out, re.DOTALL)
```

**Verification:**
```python
assert match is not None
```

### Step 7: Call monkeypatch.setattr()

```python
monkeypatch.setattr(mne.utils.config, '_get_latest_version', lambda timeout: '1.5.1')
```

### Step 8: Call monkeypatch.setattr()

```python
monkeypatch.setattr(mne, '__version__', '1.5.1')
```

### Step 9: Assign out = ClosingStringIO(...)

```python
out = ClosingStringIO()
```

### Step 10: Call sys_info()

```python
sys_info(fid=out)
```

### Step 11: Assign out = out.getvalue(...)

```python
out = out.getvalue()
```

**Verification:**
```python
assert ' 1.5.1 (latest release)' in out
```

### Step 12: Call monkeypatch.setattr()

```python
monkeypatch.setattr(mne, '__version__', '1.6.dev0')
```

### Step 13: Assign out = ClosingStringIO(...)

```python
out = ClosingStringIO()
```

### Step 14: Call sys_info()

```python
sys_info(fid=out)
```

### Step 15: Assign out = out.getvalue(...)

```python
out = out.getvalue()
```

**Verification:**
```python
assert 'development, ' in out
```

### Step 16: Call m.setattr()

```python
m.setattr(mne.utils.config, 'urlopen', partial(bad_open, msg='SSL: CERT'))
```

### Step 17: Call sys_info()

```python
sys_info(fid=out)
```

### Step 18: Call m.setattr()

```python
m.setattr(mne.utils.config, 'urlopen', partial(bad_open, msg='foo bar'))
```

### Step 19: Call sys_info()

```python
sys_info(fid=out)
```


## Complete Example

```python
# Setup
# Fixtures: monkeypatch

# Workflow
'Test other failure modes of the sys info check.'

def bad_open(url, timeout, msg):
    raise URLError(msg)
out = ClosingStringIO()
with monkeypatch.context() as m:
    m.setattr(mne.utils.config, 'urlopen', partial(bad_open, msg='SSL: CERT'))
    sys_info(fid=out)
out = out.getvalue()
assert re.match('.*unable to check.*SSL.*', out, re.DOTALL) is not None
out = ClosingStringIO()
with monkeypatch.context() as m:
    m.setattr(mne.utils.config, 'urlopen', partial(bad_open, msg='foo bar'))
    sys_info(fid=out)
out = out.getvalue()
match = re.match('.*unable to .*unknown error: .*foo bar.*', out, re.DOTALL)
assert match is not None
monkeypatch.setattr(mne.utils.config, '_get_latest_version', lambda timeout: '1.5.1')
monkeypatch.setattr(mne, '__version__', '1.5.1')
out = ClosingStringIO()
sys_info(fid=out)
out = out.getvalue()
assert ' 1.5.1 (latest release)' in out
monkeypatch.setattr(mne, '__version__', '1.6.dev0')
out = ClosingStringIO()
sys_info(fid=out)
out = out.getvalue()
assert 'development, ' in out
assert 'updating.html' not in out
```

## Next Steps


---

*Source: test_config.py:202 | Complexity: Advanced | Last updated: 2026-05-18*