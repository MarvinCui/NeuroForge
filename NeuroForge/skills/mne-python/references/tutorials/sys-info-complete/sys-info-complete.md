# How To: Sys Info Complete

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that sys_info is sufficiently complete.

## Prerequisites

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


## Step-by-Step Guide

### Step 1: 'Test that sys_info is sufficiently complete.'

```python
'Test that sys_info is sufficiently complete.'
```

**Verification:**
```python
assert f' {dep}' in out, f'Missing in dev config: {dep}'
```

### Step 2: Assign tomllib = pytest.importorskip(...)

```python
tomllib = pytest.importorskip('tomllib')
```

### Step 3: Assign pyproject = value

```python
pyproject = Path(__file__).parents[3] / 'pyproject.toml'
```

### Step 4: Assign out = ClosingStringIO(...)

```python
out = ClosingStringIO()
```

### Step 5: Call sys_info()

```python
sys_info(fid=out, check_version=False, dependencies='developer')
```

### Step 6: Assign out = out.getvalue(...)

```python
out = out.getvalue()
```

### Step 7: Assign pyproject = tomllib.loads(...)

```python
pyproject = tomllib.loads(pyproject.read_text('utf-8'))
```

### Step 8: Assign deps = value

```python
deps = [dep for dep in pyproject['dependency-groups']['test_extra'] if not isinstance(dep, dict)]
```

### Step 9: Call pytest.skip()

```python
pytest.skip('Does not appear to be a dev installation')
```

### Step 10: Assign dep = unknown.strip(...)

```python
dep = dep.split('[')[0].split('>')[0].strip()
```

**Verification:**
```python
assert f' {dep}' in out, f'Missing in dev config: {dep}'
```


## Complete Example

```python
# Workflow
'Test that sys_info is sufficiently complete.'
tomllib = pytest.importorskip('tomllib')
pyproject = Path(__file__).parents[3] / 'pyproject.toml'
if not pyproject.is_file():
    pytest.skip('Does not appear to be a dev installation')
out = ClosingStringIO()
sys_info(fid=out, check_version=False, dependencies='developer')
out = out.getvalue()
pyproject = tomllib.loads(pyproject.read_text('utf-8'))
deps = [dep for dep in pyproject['dependency-groups']['test_extra'] if not isinstance(dep, dict)]
for dep in deps:
    dep = dep.split('[')[0].split('>')[0].strip()
    assert f' {dep}' in out, f'Missing in dev config: {dep}'
```

## Next Steps


---

*Source: test_config.py:124 | Complexity: Advanced | Last updated: 2026-05-18*