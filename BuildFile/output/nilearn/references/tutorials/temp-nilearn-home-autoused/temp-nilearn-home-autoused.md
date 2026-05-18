# How To: Temp Nilearn Home Autoused

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Check that '~', NILEARN_DATA, NILEARN_SHARED_DATA        are properly expanded.
    

## Prerequisites

**Required Modules:**
- `os`
- `pathlib`
- `urllib`
- `requests`


## Step-by-Step Guide

### Step 1: "Check that '~', NILEARN_DATA, NILEARN_SHARED_DATA        are properly expanded.\n    "

```python
"Check that '~', NILEARN_DATA, NILEARN_SHARED_DATA        are properly expanded.\n    "
```

**Verification:**
```python
assert home_dir.name.startswith('temp_nilearn_home')
```

### Step 2: Assign home_dir = Path.expanduser(...)

```python
home_dir = Path('~').expanduser()
```

**Verification:**
```python
assert home_dir.name.startswith('temp_nilearn_home')
```

### Step 3: Assign home_dir = Path.home(...)

```python
home_dir = Path.home()
```

**Verification:**
```python
assert home_dir.name.startswith('temp_nilearn_home')
```

### Step 4: Assign home_dir = Path.expanduser(...)

```python
home_dir = Path('~').expanduser()
```

**Verification:**
```python
assert nilearn_data.parent.name.startswith('temp_nilearn_home')
```

### Step 5: Assign nilearn_data = Path(...)

```python
nilearn_data = Path(os.environ.get('NILEARN_DATA'))
```

**Verification:**
```python
assert nilearn_shared_data.parent.name.startswith('temp_nilearn_home')
```

### Step 6: Assign nilearn_shared_data = Path(...)

```python
nilearn_shared_data = Path(os.environ.get('NILEARN_SHARED_DATA'))
```

**Verification:**
```python
assert nilearn_shared_data.parent.name.startswith('temp_nilearn_home')
```


## Complete Example

```python
# Workflow
"Check that '~', NILEARN_DATA, NILEARN_SHARED_DATA        are properly expanded.\n    "
home_dir = Path('~').expanduser()
assert home_dir.name.startswith('temp_nilearn_home')
home_dir = Path.home()
assert home_dir.name.startswith('temp_nilearn_home')
home_dir = Path('~').expanduser()
assert home_dir.name.startswith('temp_nilearn_home')
nilearn_data = Path(os.environ.get('NILEARN_DATA'))
assert nilearn_data.parent.name.startswith('temp_nilearn_home')
nilearn_shared_data = Path(os.environ.get('NILEARN_SHARED_DATA'))
assert nilearn_shared_data.parent.name.startswith('temp_nilearn_home')
```

## Next Steps


---

*Source: test_mocking_autoused.py:42 | Complexity: Intermediate | Last updated: 2026-05-18*