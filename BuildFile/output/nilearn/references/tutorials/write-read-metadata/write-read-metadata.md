# How To: Write Read Metadata

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test _write_metadata and _add_absolute_paths.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `hashlib`
- `json`
- `os`
- `re`
- `stat`
- `pathlib`
- `urllib`
- `numpy`
- `pandas`
- `pytest`
- `requests`
- `nilearn._utils.data_gen`
- `nilearn.conftest`
- `nilearn.datasets`
- `nilearn.image`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test _write_metadata and _add_absolute_paths.'

```python
'Test _write_metadata and _add_absolute_paths.'
```

**Verification:**
```python
assert 'relative_path' in written_metadata
```

### Step 2: Assign metadata = value

```python
metadata = {'relative_path': 'collection_1', 'absolute_path': Path('tmp', 'collection_1')}
```

**Verification:**
```python
assert 'absolute_path' not in written_metadata
```

### Step 3: Assign metadata_path = value

```python
metadata_path = tmp_path / 'metadata.json'
```

**Verification:**
```python
assert read_metadata['absolute_path'] == Path('tmp', 'collection_1')
```

### Step 4: Call neurovault._write_metadata()

```python
neurovault._write_metadata(metadata, metadata_path)
```

**Verification:**
```python
assert 'relative_path' in written_metadata
```

### Step 5: Assign read_metadata = neurovault._add_absolute_paths(...)

```python
read_metadata = neurovault._add_absolute_paths(Path('tmp'), written_metadata)
```

**Verification:**
```python
assert read_metadata['absolute_path'] == Path('tmp', 'collection_1')
```

### Step 6: Assign written_metadata = json.loads(...)

```python
written_metadata = json.loads(meta_file.read().decode('utf-8'))
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test _write_metadata and _add_absolute_paths.'
metadata = {'relative_path': 'collection_1', 'absolute_path': Path('tmp', 'collection_1')}
metadata_path = tmp_path / 'metadata.json'
neurovault._write_metadata(metadata, metadata_path)
with metadata_path.open('rb') as meta_file:
    written_metadata = json.loads(meta_file.read().decode('utf-8'))
assert 'relative_path' in written_metadata
assert 'absolute_path' not in written_metadata
read_metadata = neurovault._add_absolute_paths(Path('tmp'), written_metadata)
assert read_metadata['absolute_path'] == Path('tmp', 'collection_1')
```

## Next Steps


---

*Source: test_neurovault.py:601 | Complexity: Intermediate | Last updated: 2026-05-18*