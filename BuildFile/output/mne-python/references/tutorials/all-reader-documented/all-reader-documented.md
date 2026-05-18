# How To: All Reader Documented

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that all the readers in the documentation are accepted by read_raw.

## Prerequisites

**Required Modules:**
- `pathlib`
- `shutil`
- `pytest`
- `mne.datasets`
- `mne.io`
- `mne.io._read_raw`


## Step-by-Step Guide

### Step 1: 'Test that all the readers in the documentation are accepted by read_raw.'

```python
'Test that all the readers in the documentation are accepted by read_raw.'
```

### Step 2: Assign readers = _get_supported(...)

```python
readers = _get_supported()
```

### Step 3: Assign functions = value

```python
functions = [foo.__name__ for value in readers.values() for foo in value.values()]
```

### Step 4: Assign doc_folder = value

```python
doc_folder = Path(__file__).parents[3] / 'doc'
```

### Step 5: Assign doc_file = value

```python
doc_file = doc_folder / 'api' / 'reading_raw_data.rst'
```

### Step 6: Assign doc = doc_file.read_text(...)

```python
doc = doc_file.read_text('utf-8')
```

### Step 7: Assign reader_lines = value

```python
reader_lines = [line.strip() for line in doc.split('\n') if line.strip().startswith('read_raw_')]
```

### Step 8: Assign reader_lines = value

```python
reader_lines = [elt for elt in reader_lines if elt not in reader_excluded_from_read_raw]
```

### Step 9: Assign missing_from_read_raw = value

```python
missing_from_read_raw = set(reader_lines) - set(functions)
```

### Step 10: Assign missing_from_doc = value

```python
missing_from_doc = set(functions) - set(reader_lines)
```

### Step 11: Call pytest.skip()

```python
pytest.skip('Documentation folder not found.')
```


## Complete Example

```python
# Workflow
'Test that all the readers in the documentation are accepted by read_raw.'
readers = _get_supported()
functions = [foo.__name__ for value in readers.values() for foo in value.values()]
doc_folder = Path(__file__).parents[3] / 'doc'
if not doc_folder.exists():
    pytest.skip('Documentation folder not found.')
doc_file = doc_folder / 'api' / 'reading_raw_data.rst'
doc = doc_file.read_text('utf-8')
reader_lines = [line.strip() for line in doc.split('\n') if line.strip().startswith('read_raw_')]
reader_lines = [elt for elt in reader_lines if elt not in reader_excluded_from_read_raw]
missing_from_read_raw = set(reader_lines) - set(functions)
missing_from_doc = set(functions) - set(reader_lines)
if len(missing_from_doc) != 0 or len(missing_from_read_raw) != 0:
    raise AssertionError('Functions missing from documentation of mne.io.read_raw:\n\t' + '\n\t'.join(missing_from_doc) + '\n\nFunctions missing from read_raw:\n\t' + '\n\t'.join(missing_from_read_raw))
if sorted(reader_lines) != list(reader_lines):
    raise AssertionError('Functions in documentation are not sorted. Expected order:\n\t' + '\n\t'.join(sorted(reader_lines)))
```

## Next Steps


---

*Source: test_read_raw.py:112 | Complexity: Advanced | Last updated: 2026-05-18*