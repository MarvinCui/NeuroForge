# How To: Examples Parse Correctly

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: test examples parse correctly

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
# Fixtures: monkeypatch, mocked_script
```

## Step-by-Step Guide

### Step 1: Call monkeypatch.setattr()

```python
monkeypatch.setattr(afni_test_utils.minimal_funcs_for_run_tests_cli, 'dir_path', lambda x: str(Path(x).expanduser()))
```

**Verification:**
```python
assert err.typename == 'SystemExit'
```

### Step 2: Assign stdout_ = value

```python
stdout_ = sys.stdout
```

**Verification:**
```python
assert err.value.code == 0
```

### Step 3: Call unknown.write_text()

```python
(mocked_script.parent / 'README.rst').write_text('some content')
```

### Step 4: Assign scripts_dir = value

```python
scripts_dir = mocked_script.parent / 'scripts'
```

### Step 5: Call scripts_dir.mkdir()

```python
scripts_dir.mkdir()
```

### Step 6: Call unknown.touch()

```python
(scripts_dir / 'test_ptaylor.py').touch()
```

### Step 7: Assign sys.stdout = stdout_

```python
sys.stdout = stdout_
```

### Step 8: Assign arg_list = value

```python
arg_list = shlex.split(example.splitlines()[-1])[1:]
```

### Step 9: Assign script_name = value

```python
script_name = name.replace(' ', '_') + '.py'
```

### Step 10: Assign example_script = mocked_script.with_name(...)

```python
example_script = mocked_script.with_name(f'{script_name}')
```

### Step 11: Call example_script.write_text()

```python
example_script.write_text(SCRIPT.read_text())
```

### Step 12: Call monkeypatch.setattr()

```python
monkeypatch.setattr(sys, 'argv', [example_script.name, *arg_list])
```

### Step 13: Call monkeypatch.setattr()

```python
monkeypatch.setattr(afni_test_utils.run_tests_func, 'run_tests', Mock(side_effect=SystemExit(0)))
```

### Step 14: Call monkeypatch.setattr()

```python
monkeypatch.setattr(afni_test_utils.container_execution, 'run_containerized', Mock(side_effect=SystemExit(0)))
```

### Step 15: Call monkeypatch.setattr()

```python
monkeypatch.setattr(afni_test_utils.minimal_funcs_for_run_tests_cli, 'modify_path_and_env_if_not_using_cmake', lambda *args, **kwargs: None)
```

### Step 16: Assign res = runpy.run_path(...)

```python
res = runpy.run_path(str(example_script))
```

**Verification:**
```python
assert err.typename == 'SystemExit'
```

### Step 17: Assign sys.stdout = open(...)

```python
sys.stdout = open(os.devnull, 'w')
```

### Step 18: Call unknown()

```python
res['main']()
```

### Step 19: Assign sys.stdout = stdout_

```python
sys.stdout = stdout_
```

### Step 20: Call unknown.assert_called_once()

```python
res['main'].__globals__['run_tests'].assert_called_once()
```

### Step 21: Call unknown.assert_called_once()

```python
res['main'].__globals__['run_containerized'].assert_called_once()
```


## Complete Example

```python
# Setup
# Fixtures: monkeypatch, mocked_script

# Workflow
monkeypatch.setattr(afni_test_utils.minimal_funcs_for_run_tests_cli, 'dir_path', lambda x: str(Path(x).expanduser()))
stdout_ = sys.stdout
(mocked_script.parent / 'README.rst').write_text('some content')
scripts_dir = mocked_script.parent / 'scripts'
scripts_dir.mkdir()
(scripts_dir / 'test_ptaylor.py').touch()
for name, example in run_tests_examples.examples.items():
    arg_list = shlex.split(example.splitlines()[-1])[1:]
    script_name = name.replace(' ', '_') + '.py'
    example_script = mocked_script.with_name(f'{script_name}')
    example_script.write_text(SCRIPT.read_text())
    monkeypatch.setattr(sys, 'argv', [example_script.name, *arg_list])
    monkeypatch.setattr(afni_test_utils.run_tests_func, 'run_tests', Mock(side_effect=SystemExit(0)))
    monkeypatch.setattr(afni_test_utils.container_execution, 'run_containerized', Mock(side_effect=SystemExit(0)))
    monkeypatch.setattr(afni_test_utils.minimal_funcs_for_run_tests_cli, 'modify_path_and_env_if_not_using_cmake', lambda *args, **kwargs: None)
    res = runpy.run_path(str(example_script))
    with pytest.raises(SystemExit) as err:
        sys.stdout = open(os.devnull, 'w')
        res['main']()
        sys.stdout = stdout_
    assert err.typename == 'SystemExit'
    assert err.value.code == 0
    if 'local' in arg_list:
        res['main'].__globals__['run_tests'].assert_called_once()
    elif 'container' in arg_list:
        res['main'].__globals__['run_containerized'].assert_called_once()
sys.stdout = stdout_
```

## Next Steps


---

*Source: test_testing_script_functionality.py:964 | Complexity: Advanced | Last updated: 2026-05-18*