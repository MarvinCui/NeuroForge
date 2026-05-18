# How To: Run Cmd Timeout

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: test run cmd timeout

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `argparse`
- `collections`
- `pathlib`
- `pathlib`
- `unittest.mock`
- `importlib`
- `logging`
- `os`
- `pytest`
- `runpy`
- `shlex`
- `shutil`
- `subprocess`
- `subprocess`
- `signal`
- `sys`
- `tempfile`
- `time`
- `io`
- `contextlib`
- `contextlib`
- `afni_test_utils`
- `afni_test_utils`
- `afni_test_utils`
- `afni_test_utils`
- `afni_test_utils`
- `afni_test_utils.misc`
- `afnipy`
- `afni_test_utils`

**Setup Required:**
```python
# Fixtures: data, monkeypatch
```

## Step-by-Step Guide

### Step 1: Assign data.logger = logging

```python
data.logger = logging
```

**Verification:**
```python
assert delta_t < t_unit + 1.1
```

### Step 2: Call monkeypatch.setattr()

```python
monkeypatch.setattr(logging, 'warn', lambda x: None)
```

**Verification:**
```python
assert stdout_log.read_text() == 'hello\n'
```

### Step 3: Assign t_unit = 0.2

```python
t_unit = 0.2
```

### Step 4: Call tools.run_cmd()

```python
tools.run_cmd(data, f'sleep {t_unit * 10} & sleep {t_unit}; kill %1', timeout=t_unit * 2)
```

### Step 5: Assign start = time.time(...)

```python
start = time.time()
```

### Step 6: Assign start = time.time(...)

```python
start = time.time()
```

### Step 7: Assign delta_t = value

```python
delta_t = time.time() - start
```

**Verification:**
```python
assert delta_t < t_unit + 1.1
```

### Step 8: Assign unknown = tools.run_cmd(...)

```python
stdout_log, stderr_log = tools.run_cmd(data, f'sleep {t_unit / 2}; echo hello & sleep {t_unit / 5}', timeout=t_unit * 1)
```

**Verification:**
```python
assert stdout_log.read_text() == 'hello\n'
```

### Step 9: Call tools.run_cmd()

```python
tools.run_cmd(data, f'sleep {t_unit} & sleep {t_unit}', timeout=t_unit * 0.5)
```

### Step 10: Call tools.run_cmd()

```python
tools.run_cmd(data, f'sleep {t_unit * 500} & sleep {t_unit / 2}', timeout=t_unit)
```


## Complete Example

```python
# Setup
# Fixtures: data, monkeypatch

# Workflow
data.logger = logging
monkeypatch.setattr(logging, 'warn', lambda x: None)
t_unit = 0.2
tools.run_cmd(data, f'sleep {t_unit * 10} & sleep {t_unit}; kill %1', timeout=t_unit * 2)
start = time.time()
with pytest.raises(TimeoutError):
    tools.run_cmd(data, f'sleep {t_unit} & sleep {t_unit}', timeout=t_unit * 0.5)
start = time.time()
with pytest.raises(TimeoutError):
    tools.run_cmd(data, f'sleep {t_unit * 500} & sleep {t_unit / 2}', timeout=t_unit)
delta_t = time.time() - start
assert delta_t < t_unit + 1.1
stdout_log, stderr_log = tools.run_cmd(data, f'sleep {t_unit / 2}; echo hello & sleep {t_unit / 5}', timeout=t_unit * 1)
assert stdout_log.read_text() == 'hello\n'
```

## Next Steps


---

*Source: test_testing_script_functionality.py:171 | Complexity: Advanced | Last updated: 2026-05-18*