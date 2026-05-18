# How To: Rewrite Paths For Line Error

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: If the the stdout or stderr stream  output directories returned from get_command_info_dicts

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

### Step 1: '\n    If the the stdout or stderr stream  output directories returned from get_command_info_dicts\n    '

```python
'\n    If the the stdout or stderr stream  output directories returned from get_command_info_dicts\n    '
```

### Step 2: Assign cmd_info = defaultdict(...)

```python
cmd_info = defaultdict(lambda: '')
```

### Step 3: Assign unknown = '/a/base/path/output_of_tests/output_2020_11_12_154136'

```python
cmd_info['outdir'] = '/a/base/path/output_of_tests/output_2020_11_12_154136'
```

### Step 4: Assign unknown = '/a/base/path'

```python
cmd_info['workdir'] = '/a/base/path'
```

### Step 5: Assign unknown = '/a/base/path'

```python
cmd_info['tests_data_dir'] = '/a/base/path'
```

### Step 6: Call monkeypatch.setattr()

```python
monkeypatch.setattr(tools, 'get_command_info_dicts', Mock(return_value=[cmd_info, defaultdict(lambda: '')]))
```

### Step 7: Assign txt = value

```python
txt = ['/a/base/path/output_of_tests/output_2020_11_12_154142/subdir other text']
```

### Step 8: Assign unknown = '/a/different/base/path/output_of_tests/output_2020_11_12_154136'

```python
cmd_info['outdir'] = '/a/different/base/path/output_of_tests/output_2020_11_12_154136'
```

### Step 9: Assign modified_line = tools.rewrite_paths_for_cleaner_diffs(...)

```python
modified_line = tools.rewrite_paths_for_cleaner_diffs(data, [txt])
```

### Step 10: Assign modified_line = tools.rewrite_paths_for_cleaner_diffs(...)

```python
modified_line = tools.rewrite_paths_for_cleaner_diffs(data, [txt])
```


## Complete Example

```python
# Setup
# Fixtures: data, monkeypatch

# Workflow
'\n    If the the stdout or stderr stream  output directories returned from get_command_info_dicts\n    '
cmd_info = defaultdict(lambda: '')
cmd_info['outdir'] = '/a/base/path/output_of_tests/output_2020_11_12_154136'
cmd_info['workdir'] = '/a/base/path'
cmd_info['tests_data_dir'] = '/a/base/path'
monkeypatch.setattr(tools, 'get_command_info_dicts', Mock(return_value=[cmd_info, defaultdict(lambda: '')]))
txt = ['/a/base/path/output_of_tests/output_2020_11_12_154142/subdir other text']
with pytest.raises(ValueError):
    modified_line = tools.rewrite_paths_for_cleaner_diffs(data, [txt])
cmd_info['outdir'] = '/a/different/base/path/output_of_tests/output_2020_11_12_154136'
with pytest.raises(ValueError):
    modified_line = tools.rewrite_paths_for_cleaner_diffs(data, [txt])
```

## Next Steps


---

*Source: test_testing_script_functionality.py:617 | Complexity: Advanced | Last updated: 2026-05-18*