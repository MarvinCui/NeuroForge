# How To: Nodeexecutionerror

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: test NodeExecutionError

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `copy`
- `pytest`
- `interfaces`
- `interfaces`
- `utils`
- `test_base`
- `test_utils`
- `nipype`
- `nipype`
- `nipype`
- `nipype.interfaces.utility`
- `nipype.pipeline.plugins.base`
- `stat`
- `os`

**Setup Required:**
```python
# Fixtures: tmp_path, monkeypatch
```

## Step-by-Step Guide

### Step 1: Call monkeypatch.chdir()

```python
monkeypatch.chdir(tmp_path)
```

**Verification:**
```python
assert attr in error_msg
```

### Step 2: Assign exebin = value

```python
exebin = tmp_path / 'bin'
```

**Verification:**
```python
assert 'This should fail' in error_msg
```

### Step 3: Call exebin.mkdir()

```python
exebin.mkdir()
```

**Verification:**
```python
assert 'Traceback:' in error_msg
```

### Step 4: Assign exe = value

```python
exe = exebin / 'nipype-node-execution-fail'
```

**Verification:**
```python
assert 'Cmdline:' not in error_msg
```

### Step 5: Call exe.write_text()

```python
exe.write_text('#!/bin/bash\necho "Running"\necho "This should fail" >&2\nexit 1', encoding='utf-8')
```

**Verification:**
```python
assert 'Functions can fail too' in error_msg
```

### Step 6: Call exe.chmod()

```python
exe.chmod(exe.stat().st_mode | stat.S_IEXEC)
```

### Step 7: Call monkeypatch.setenv()

```python
monkeypatch.setenv('PATH', str(exe.parent.absolute()), prepend=os.pathsep)
```

### Step 8: Assign cmd = pe.Node(...)

```python
cmd = pe.Node(FailCommandLine(), name='cmd-fail', base_dir='cmd')
```

### Step 9: Assign error_msg = str(...)

```python
error_msg = str(exc.value)
```

**Verification:**
```python
assert 'This should fail' in error_msg
```

### Step 10: Assign func = pe.Node(...)

```python
func = pe.Node(niu.Function(function=fail), name='func-fail', base_dir='func')
```

### Step 11: Assign error_msg = str(...)

```python
error_msg = str(exc.value)
```

**Verification:**
```python
assert 'Traceback:' in error_msg
```

### Step 12: Call cmd.run()

```python
cmd.run()
```

**Verification:**
```python
assert attr in error_msg
```

### Step 13: Call func.run()

```python
func.run()
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, monkeypatch

# Workflow
import stat
monkeypatch.chdir(tmp_path)
exebin = tmp_path / 'bin'
exebin.mkdir()
exe = exebin / 'nipype-node-execution-fail'
exe.write_text('#!/bin/bash\necho "Running"\necho "This should fail" >&2\nexit 1', encoding='utf-8')
exe.chmod(exe.stat().st_mode | stat.S_IEXEC)
monkeypatch.setenv('PATH', str(exe.parent.absolute()), prepend=os.pathsep)
cmd = pe.Node(FailCommandLine(), name='cmd-fail', base_dir='cmd')
with pytest.raises(pe.nodes.NodeExecutionError) as exc:
    cmd.run()
error_msg = str(exc.value)
for attr in ('Cmdline:', 'Stdout:', 'Stderr:', 'Traceback:'):
    assert attr in error_msg
assert 'This should fail' in error_msg

def fail():
    raise Exception('Functions can fail too')
func = pe.Node(niu.Function(function=fail), name='func-fail', base_dir='func')
with pytest.raises(pe.nodes.NodeExecutionError) as exc:
    func.run()
error_msg = str(exc.value)
assert 'Traceback:' in error_msg
assert 'Cmdline:' not in error_msg
assert 'Functions can fail too' in error_msg
```

## Next Steps


---

*Source: test_nodes.py:345 | Complexity: Advanced | Last updated: 2026-05-18*