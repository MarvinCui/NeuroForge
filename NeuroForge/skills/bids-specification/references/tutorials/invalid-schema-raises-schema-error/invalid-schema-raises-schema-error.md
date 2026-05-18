# How To: Invalid Schema Raises Schema Error

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Configuration example: Provide an invalid schema, ensuring that 'SchemaError' is raised.

## Prerequisites

**Required Modules:**
- `contextlib`
- `typing`
- `pytest`
- `jsonschema.exceptions`
- `jsonschema.protocols`
- `jsonschema.validators`
- `bidsschematools.utils`


## Step-by-Step Guide

### Step 1: Assign invalid_schema = value

```python
invalid_schema = {'$schema': 'https://json-schema.org/draft/2020-12/schema', 'type': 123}
```


## Complete Example

```python
# Workflow
invalid_schema = {'$schema': 'https://json-schema.org/draft/2020-12/schema', 'type': 123}
```

## Next Steps


---

*Source: test_utils.py:142 | Complexity: Beginner | Last updated: 2026-05-18*