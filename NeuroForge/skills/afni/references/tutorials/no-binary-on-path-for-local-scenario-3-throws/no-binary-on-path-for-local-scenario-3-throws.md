# How To: No Binary On Path For Local Scenario 3 Throws

**Difficulty**: Intermediate
**Estimated Time**: 5 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: test no binary on path for local scenario 3 throws

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
# Fixtures: monkeypatch
```

## Step-by-Step Guide

### Step 1: Call monkeypatch.setenv()

```python
monkeypatch.setenv('PATH', minfuncs.filter_afni_from_path())
```

**Verification:**
```python
assert 'Cannot find local AFNI binaries. ' == str(e.value)
```

### Step 2: Call monkeypatch.setattr()

```python
monkeypatch.setattr(afni_test_utils.minimal_funcs_for_run_tests_cli, 'make_sure_afnipy_not_importable', lambda: True)
```

**Verification:**
```python
assert 'Cannot find local AFNI binaries. ' == str(e.value)
```

### Step 3: Call minfuncs.modify_path_and_env_if_not_using_cmake()

```python
minfuncs.modify_path_and_env_if_not_using_cmake()
```


## Complete Example

```python
# Setup
# Fixtures: monkeypatch

# Workflow
monkeypatch.setenv('PATH', minfuncs.filter_afni_from_path())
monkeypatch.setattr(afni_test_utils.minimal_funcs_for_run_tests_cli, 'make_sure_afnipy_not_importable', lambda: True)
with pytest.raises(EnvironmentError) as e:
    minfuncs.modify_path_and_env_if_not_using_cmake()
assert 'Cannot find local AFNI binaries. ' == str(e.value)
```

## Next Steps


---

*Source: test_testing_script_functionality.py:1514 | Complexity: Intermediate | Last updated: 2026-05-18*