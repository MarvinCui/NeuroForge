# How To: Unparse Args For Container

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test unparse args for container

## Prerequisites

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


## Step-by-Step Guide

### Step 1: Assign user_args = value

```python
user_args = {}
```

**Verification:**
```python
assert converted == expected
```

### Step 2: Assign expected = ' local'

```python
expected = ' local'
```

**Verification:**
```python
assert converted == expected
```

### Step 3: Assign converted = ce.unparse_args_for_container(...)

```python
converted = ce.unparse_args_for_container(TESTS_DIR, **user_args)
```

**Verification:**
```python
assert converted == expected
```

### Step 4: Assign user_args = value

```python
user_args = {'build_dir': '/saved/afni/build', 'debug': True, 'extra_args': None, 'ignore_dirty_data': False, 'image_name': 'afni/afni_cmake_build', 'source_mode': 'host', 'only_use_local': True, 'use_all_cores': False, 'coverage': True, 'verbose': False}
```

**Verification:**
```python
assert '--arbitrary-kwarg-with-underscores local' in converted
```

### Step 5: Assign expected = ' --build-dir=/opt/afni/build --debug --coverage local'

```python
expected = ' --build-dir=/opt/afni/build --debug --coverage local'
```

**Verification:**
```python
assert '--build-dir=/opt/afni/build' in converted
```

### Step 6: Assign converted = ce.unparse_args_for_container(...)

```python
converted = ce.unparse_args_for_container(TESTS_DIR, **user_args)
```

**Verification:**
```python
assert converted == expected
```

### Step 7: Assign user_args = value

```python
user_args = {'debug': False, 'extra_args': '-k hello --trace', 'use_all_cores': False, 'coverage': True, 'verbose': False}
```

### Step 8: Assign expected = ' --extra-args="-k hello --trace" --coverage local'

```python
expected = ' --extra-args="-k hello --trace" --coverage local'
```

### Step 9: Assign converted = ce.unparse_args_for_container(...)

```python
converted = ce.unparse_args_for_container(TESTS_DIR, **user_args)
```

**Verification:**
```python
assert converted == expected
```

### Step 10: Assign user_args = value

```python
user_args = {'arbitrary_kwarg_with_underscores': True}
```

### Step 11: Assign converted = ce.unparse_args_for_container(...)

```python
converted = ce.unparse_args_for_container(TESTS_DIR, **user_args)
```

**Verification:**
```python
assert '--arbitrary-kwarg-with-underscores local' in converted
```

### Step 12: Assign user_args = value

```python
user_args = {'reuse_build': True}
```

### Step 13: Assign converted = ce.unparse_args_for_container(...)

```python
converted = ce.unparse_args_for_container(TESTS_DIR, **user_args)
```

**Verification:**
```python
assert '--build-dir=/opt/afni/build' in converted
```


## Complete Example

```python
# Workflow
user_args = {}
expected = ' local'
converted = ce.unparse_args_for_container(TESTS_DIR, **user_args)
assert converted == expected
user_args = {'build_dir': '/saved/afni/build', 'debug': True, 'extra_args': None, 'ignore_dirty_data': False, 'image_name': 'afni/afni_cmake_build', 'source_mode': 'host', 'only_use_local': True, 'use_all_cores': False, 'coverage': True, 'verbose': False}
expected = ' --build-dir=/opt/afni/build --debug --coverage local'
converted = ce.unparse_args_for_container(TESTS_DIR, **user_args)
assert converted == expected
user_args = {'debug': False, 'extra_args': '-k hello --trace', 'use_all_cores': False, 'coverage': True, 'verbose': False}
expected = ' --extra-args="-k hello --trace" --coverage local'
converted = ce.unparse_args_for_container(TESTS_DIR, **user_args)
assert converted == expected
user_args = {'arbitrary_kwarg_with_underscores': True}
converted = ce.unparse_args_for_container(TESTS_DIR, **user_args)
assert '--arbitrary-kwarg-with-underscores local' in converted
user_args = {'reuse_build': True}
converted = ce.unparse_args_for_container(TESTS_DIR, **user_args)
assert '--build-dir=/opt/afni/build' in converted
```

## Next Steps


---

*Source: test_testing_script_functionality.py:1211 | Complexity: Advanced | Last updated: 2026-05-18*