# How To: Profile Parse

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test profile parse

## Prerequisites

**Required Modules:**
- `snakemake.cli`
- `io`
- `snakemake.profiles`
- `textwrap`
- `pytest`
- `snakemake.pathvars`
- `snakemake.ioutils`
- `snakemake.iocontainers`
- `snakemake_interface_common.exceptions`


## Step-by-Step Guide

### Step 1: Assign profile = textwrap.dedent(...)

```python
profile = textwrap.dedent('\n    set-resources:\n        rule1:\n            slurm_partition: "42"\n    ')
```

**Verification:**
```python
assert parsed_profile == {'set-resources': ["rule1:slurm_partition='42'"]}
```

### Step 2: Assign stream = StringIO(...)

```python
stream = StringIO(profile)
```

**Verification:**
```python
assert parsed_resources['rule1']['slurm_partition'].evaluate(None, None, None, None, None, None).value == '42'
```

### Step 3: Assign stream.name = 'foo/config.yaml'

```python
stream.name = 'foo/config.yaml'
```

### Step 4: Assign parsed_profile = ProfileConfigFileParser.parse(...)

```python
parsed_profile = ProfileConfigFileParser().parse(stream)
```

**Verification:**
```python
assert parsed_profile == {'set-resources': ["rule1:slurm_partition='42'"]}
```

### Step 5: Assign parsed_resources = parse_set_resources(...)

```python
parsed_resources = parse_set_resources(parsed_profile['set-resources'])
```

**Verification:**
```python
assert parsed_resources['rule1']['slurm_partition'].evaluate(None, None, None, None, None, None).value == '42'
```


## Complete Example

```python
# Workflow
profile = textwrap.dedent('\n    set-resources:\n        rule1:\n            slurm_partition: "42"\n    ')
stream = StringIO(profile)
stream.name = 'foo/config.yaml'
parsed_profile = ProfileConfigFileParser().parse(stream)
assert parsed_profile == {'set-resources': ["rule1:slurm_partition='42'"]}
parsed_resources = parse_set_resources(parsed_profile['set-resources'])
assert parsed_resources['rule1']['slurm_partition'].evaluate(None, None, None, None, None, None).value == '42'
```

## Next Steps


---

*Source: test_internals.py:91 | Complexity: Intermediate | Last updated: 2026-05-18*