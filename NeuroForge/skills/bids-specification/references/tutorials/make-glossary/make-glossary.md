# How To: Make Glossary

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test whether files under the schema objects subdirectory correspond to entries, and
that rules are not misloaded as objects.
This may need to be updated for schema hierarchy changes.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `pytest`
- `bidsschematools.render`

**Setup Required:**
```python
# Fixtures: schema_obj, schema_dir
```

## Step-by-Step Guide

### Step 1: '\n    Test whether files under the schema objects subdirectory correspond to entries, and\n    that rules are not misloaded as objects.\n    This may need to be updated for schema hierarchy changes.\n    '

```python
'\n    Test whether files under the schema objects subdirectory correspond to entries, and\n    that rules are not misloaded as objects.\n    This may need to be updated for schema hierarchy changes.\n    '
```

**Verification:**
```python
assert any((line.startswith(f'<a name="objects.{i}.') for i in object_files))
```

### Step 2: Assign object_files = value

```python
object_files = []
```

**Verification:**
```python
assert not any((line.startswith(f'<a name="objects.{i}.') for i in rules_only))
```

### Step 3: Assign rule_files = value

```python
rule_files = []
```

### Step 4: Assign rules_only = list(...)

```python
rules_only = list(filter(lambda a: a not in object_files, rule_files))
```

### Step 5: Assign glossary = text.make_glossary(...)

```python
glossary = text.make_glossary(schema_obj)
```

**Verification:**
```python
assert any((line.startswith(f'<a name="objects.{i}.') for i in object_files))
```

### Step 6: Assign unknown = os.path.splitext(...)

```python
object_base, _ = os.path.splitext(object_file)
```

### Step 7: Call object_files.append()

```python
object_files.append(object_base)
```

### Step 8: Assign unknown = os.path.splitext(...)

```python
rule_base, _ = os.path.splitext(rule_file)
```

### Step 9: Call rule_files.append()

```python
rule_files.append(rule_base)
```


## Complete Example

```python
# Setup
# Fixtures: schema_obj, schema_dir

# Workflow
'\n    Test whether files under the schema objects subdirectory correspond to entries, and\n    that rules are not misloaded as objects.\n    This may need to be updated for schema hierarchy changes.\n    '
object_files = []
for root, dirs, files in os.walk(schema_dir, topdown=False):
    if 'objects' in root:
        for object_file in files:
            object_base, _ = os.path.splitext(object_file)
            object_files.append(object_base)
rule_files = []
for root, dirs, files in os.walk(schema_dir, topdown=False):
    if 'rules' in root:
        for rule_file in files:
            rule_base, _ = os.path.splitext(rule_file)
            rule_files.append(rule_base)
rules_only = list(filter(lambda a: a not in object_files, rule_files))
glossary = text.make_glossary(schema_obj)
for line in glossary.split('\n'):
    if line.startswith('<a name="objects.'):
        assert any((line.startswith(f'<a name="objects.{i}.') for i in object_files))
        assert not any((line.startswith(f'<a name="objects.{i}.') for i in rules_only))
```

## Next Steps


---

*Source: test_render_text.py:38 | Complexity: Advanced | Last updated: 2026-05-18*