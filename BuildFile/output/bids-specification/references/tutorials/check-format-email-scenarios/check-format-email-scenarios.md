# How To: Check Format Email Scenarios

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Parametrized test for check_format usage on valid/invalid email addresses under
Draft202012Validator.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `contextlib`
- `typing`
- `pytest`
- `jsonschema.exceptions`
- `jsonschema.protocols`
- `jsonschema.validators`
- `bidsschematools.utils`

**Setup Required:**
```python
# Fixtures: check_format, instance, expect_raises
```

## Step-by-Step Guide

### Step 1: '\n        Parametrized test for check_format usage on valid/invalid email addresses under\n        Draft202012Validator.\n        '

```python
'\n        Parametrized test for check_format usage on valid/invalid email addresses under\n        Draft202012Validator.\n        '
```

### Step 2: Assign validator = jsonschema_validator(...)

```python
validator = jsonschema_validator(DRAFT_202012_FORMAT_SCHEMA, check_format=check_format)
```

### Step 3: Assign ctx = value

```python
ctx = pytest.raises(ValidationError) if expect_raises else nullcontext()
```

### Step 4: Call validator.validate()

```python
validator.validate(instance)
```


## Complete Example

```python
# Setup
# Fixtures: check_format, instance, expect_raises

# Workflow
'\n        Parametrized test for check_format usage on valid/invalid email addresses under\n        Draft202012Validator.\n        '
validator = jsonschema_validator(DRAFT_202012_FORMAT_SCHEMA, check_format=check_format)
ctx = pytest.raises(ValidationError) if expect_raises else nullcontext()
with ctx:
    validator.validate(instance)
```

## Next Steps


---

*Source: test_utils.py:90 | Complexity: Intermediate | Last updated: 2026-05-18*