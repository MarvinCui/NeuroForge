# How To: Setup Data Vol

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: test setup test data vol

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

### Step 1: Assign unknown = get_mocked_docker(...)

```python
mocked_docker, client, _ = get_mocked_docker()
```

**Verification:**
```python
assert '-u 1000 -g 100' in init_cmd
```

### Step 2: Call ce.setup_test_data_vol()

```python
ce.setup_test_data_vol(client, {}, {}, tempfile.mkdtemp(), '/mnt')
```

**Verification:**
```python
assert '-u 1007 -g 3000' in init_cmd
```

### Step 3: Assign init_cmd = value

```python
init_cmd = client.api.create_container.call_args_list[0][0][1][2]
```

**Verification:**
```python
assert '-u 1000 -g 100' in init_cmd
```

### Step 4: Assign unknown = get_mocked_docker(...)

```python
mocked_docker, client, _ = get_mocked_docker()
```

### Step 5: Call ce.setup_test_data_vol()

```python
ce.setup_test_data_vol(client, {}, {'CONTAINER_UID': 1007, 'CONTAINER_GID': 3000}, tempfile.mkdtemp(), '/mnt')
```

### Step 6: Assign init_cmd = value

```python
init_cmd = client.api.create_container.call_args_list[0][0][1][2]
```

**Verification:**
```python
assert '-u 1007 -g 3000' in init_cmd
```


## Complete Example

```python
# Workflow
mocked_docker, client, _ = get_mocked_docker()
ce.setup_test_data_vol(client, {}, {}, tempfile.mkdtemp(), '/mnt')
init_cmd = client.api.create_container.call_args_list[0][0][1][2]
assert '-u 1000 -g 100' in init_cmd
mocked_docker, client, _ = get_mocked_docker()
ce.setup_test_data_vol(client, {}, {'CONTAINER_UID': 1007, 'CONTAINER_GID': 3000}, tempfile.mkdtemp(), '/mnt')
init_cmd = client.api.create_container.call_args_list[0][0][1][2]
assert '-u 1007 -g 3000' in init_cmd
```

## Next Steps


---

*Source: test_testing_script_functionality.py:1298 | Complexity: Intermediate | Last updated: 2026-05-18*