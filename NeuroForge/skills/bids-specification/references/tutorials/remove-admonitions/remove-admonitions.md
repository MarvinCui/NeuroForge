# How To: Remove Admonitions

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test remove admonitions

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `remove_admonitions`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: Assign input_folder = value

```python
input_folder = Path(__file__).parent / 'tests' / 'data' / 'input'
```

**Verification:**
```python
assert generated_line == expected_line
```

### Step 2: Assign expected_folder = value

```python
expected_folder = Path(__file__).parent / 'tests' / 'data' / 'expected'
```

### Step 3: Call remove_admonitions()

```python
remove_admonitions(input_folder, tmp_path)
```

### Step 4: Assign generated_files = list(...)

```python
generated_files = list(tmp_path.glob('**/*.md'))
```

### Step 5: Assign expected = value

```python
expected = expected_folder / file.relative_to(tmp_path)
```

### Step 6: Assign expected_content = f.readlines(...)

```python
expected_content = f.readlines()
```

### Step 7: Assign generated_content = f.readlines(...)

```python
generated_content = f.readlines()
```

**Verification:**
```python
assert generated_line == expected_line
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
input_folder = Path(__file__).parent / 'tests' / 'data' / 'input'
expected_folder = Path(__file__).parent / 'tests' / 'data' / 'expected'
remove_admonitions(input_folder, tmp_path)
generated_files = list(tmp_path.glob('**/*.md'))
for file in generated_files:
    expected = expected_folder / file.relative_to(tmp_path)
    with open(expected, 'r', encoding='utf8') as f:
        expected_content = f.readlines()
    with open(file, 'r', encoding='utf8') as f:
        generated_content = f.readlines()
    for expected_line, generated_line in zip(expected_content, generated_content):
        assert generated_line == expected_line
```

## Next Steps


---

*Source: test_remove_admonitions.py:6 | Complexity: Intermediate | Last updated: 2026-05-18*