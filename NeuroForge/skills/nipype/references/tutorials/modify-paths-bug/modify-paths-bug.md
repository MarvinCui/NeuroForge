# How To: Modify Paths Bug

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: There was a bug in which, if the current working directory contained a file with the name
of an output String, the string would get transformed into a path, and generally wreak havoc.
This attempts to replicate that condition, using an object with strings and paths in various
trait configurations, to ensure that the guards added resolve the issue.
Please see https://github.com/nipy/nipype/issues/2944 for more details.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `copy`
- `pytest`
- `interfaces`
- `interfaces`
- `utils`
- `shutil`
- `numpy`

**Setup Required:**
```python
# Fixtures: tmpdir
```

## Step-by-Step Guide

### Step 1: '\n    There was a bug in which, if the current working directory contained a file with the name\n    of an output String, the string would get transformed into a path, and generally wreak havoc.\n    This attempts to replicate that condition, using an object with strings and paths in various\n    trait configurations, to ensure that the guards added resolve the issue.\n    Please see https://github.com/nipy/nipype/issues/2944 for more details.\n    '

```python
'\n    There was a bug in which, if the current working directory contained a file with the name\n    of an output String, the string would get transformed into a path, and generally wreak havoc.\n    This attempts to replicate that condition, using an object with strings and paths in various\n    trait configurations, to ensure that the guards added resolve the issue.\n    Please see https://github.com/nipy/nipype/issues/2944 for more details.\n    '
```

**Verification:**
```python
assert out_str == '2'
```

### Step 2: Call tmpdir.chdir()

```python
tmpdir.chdir()
```

**Verification:**
```python
assert os.path.isabs(out_path)
```

### Step 3: Assign spc = pe.Node(...)

```python
spc = pe.Node(StrPathConfuser(in_str='2'), name='spc')
```

**Verification:**
```python
assert outputs.out_tuple == (out_path, out_str)
```

### Step 4: Call open.close()

```python
open('2', 'w').close()
```

**Verification:**
```python
assert outputs.out_dict_path == {out_str: out_path}
```

### Step 5: Assign outputs = value

```python
outputs = spc.run().outputs
```

**Verification:**
```python
assert outputs.out_dict_str == {out_str: out_str}
```

### Step 6: Assign out_str = value

```python
out_str = outputs.out_str
```

**Verification:**
```python
assert outputs.out_list == [out_str] * 2
```

### Step 7: Assign out_path = value

```python
out_path = outputs.out_path
```

**Verification:**
```python
assert os.path.isabs(out_path)
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir

# Workflow
'\n    There was a bug in which, if the current working directory contained a file with the name\n    of an output String, the string would get transformed into a path, and generally wreak havoc.\n    This attempts to replicate that condition, using an object with strings and paths in various\n    trait configurations, to ensure that the guards added resolve the issue.\n    Please see https://github.com/nipy/nipype/issues/2944 for more details.\n    '
tmpdir.chdir()
spc = pe.Node(StrPathConfuser(in_str='2'), name='spc')
open('2', 'w').close()
outputs = spc.run().outputs
out_str = outputs.out_str
assert out_str == '2'
out_path = outputs.out_path
assert os.path.isabs(out_path)
assert outputs.out_tuple == (out_path, out_str)
assert outputs.out_dict_path == {out_str: out_path}
assert outputs.out_dict_str == {out_str: out_str}
assert outputs.out_list == [out_str] * 2
```

## Next Steps


---

*Source: test_utils.py:257 | Complexity: Intermediate | Last updated: 2026-05-18*