# How To: Entity Rule

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test entity rule

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `re`
- `bidsschematools`
- `types`

**Setup Required:**
```python
# Fixtures: schema_obj
```

## Step-by-Step Guide

### Step 1: Assign rule = Namespace.build(...)

```python
rule = Namespace.build({'datatypes': ['anat'], 'entities': {'subject': 'required', 'session': 'optional'}, 'suffixes': ['T1w'], 'extensions': ['.nii']})
```

**Verification:**
```python
assert nii_rule == {'regex': 'sub-(?P<subject>[0-9a-zA-Z+]+)/(?:ses-(?P<session>[0-9a-zA-Z+]+)/)?(?P<datatype>anat)/(?(subject)sub-(?P=subject)_)(?(session)ses-(?P=session)_)(?P<suffix>T1w)(?P<extension>\\.nii)\\Z', 'mandatory': False}
```

### Step 2: Assign nii_rule = rules._entity_rule(...)

```python
nii_rule = rules._entity_rule(rule, schema_obj)
```

**Verification:**
```python
assert re.match(nii_rule['regex'], 'sub-01/anat/sub-01_T1w.nii')
```

### Step 3: Assign rule = Namespace.build(...)

```python
rule = Namespace.build({'datatypes': ['anat', ''], 'entities': {'subject': 'optional', 'session': 'optional'}, 'suffixes': ['T1w'], 'extensions': ['.json']})
```

**Verification:**
```python
assert re.match(nii_rule['regex'], 'sub-01/ses-01/anat/sub-01_ses-01_T1w.nii')
```

### Step 4: Assign json_rule = rules._entity_rule(...)

```python
json_rule = rules._entity_rule(rule, schema_obj)
```

**Verification:**
```python
assert not re.match(nii_rule['regex'], 'sub-01/anat/sub-02_T1w.nii')
```


## Complete Example

```python
# Setup
# Fixtures: schema_obj

# Workflow
rule = Namespace.build({'datatypes': ['anat'], 'entities': {'subject': 'required', 'session': 'optional'}, 'suffixes': ['T1w'], 'extensions': ['.nii']})
nii_rule = rules._entity_rule(rule, schema_obj)
assert nii_rule == {'regex': 'sub-(?P<subject>[0-9a-zA-Z+]+)/(?:ses-(?P<session>[0-9a-zA-Z+]+)/)?(?P<datatype>anat)/(?(subject)sub-(?P=subject)_)(?(session)ses-(?P=session)_)(?P<suffix>T1w)(?P<extension>\\.nii)\\Z', 'mandatory': False}
assert re.match(nii_rule['regex'], 'sub-01/anat/sub-01_T1w.nii')
assert re.match(nii_rule['regex'], 'sub-01/ses-01/anat/sub-01_ses-01_T1w.nii')
assert not re.match(nii_rule['regex'], 'sub-01/anat/sub-02_T1w.nii')
assert not re.match(nii_rule['regex'], 'sub-01/sub-01_T1w.nii')
assert not re.match(nii_rule['regex'], 'sub-01_T1w.nii')
assert not re.match(nii_rule['regex'], 'sub-01/ses-01/anat/sub-01_T1w.nii')
assert not re.match(nii_rule['regex'], 'sub-01/anat/sub-01_ses-01_T1w.nii')
assert not re.match(nii_rule['regex'], 'sub-01/ses-01/anat/sub-01_ses-02_T1w.nii')
rule = Namespace.build({'datatypes': ['anat', ''], 'entities': {'subject': 'optional', 'session': 'optional'}, 'suffixes': ['T1w'], 'extensions': ['.json']})
json_rule = rules._entity_rule(rule, schema_obj)
assert json_rule == {'regex': '(?:sub-(?P<subject>[0-9a-zA-Z+]+)/)?(?:ses-(?P<session>[0-9a-zA-Z+]+)/)?(?:(?P<datatype>anat)/)?(?(subject)sub-(?P=subject)_)(?(session)ses-(?P=session)_)(?P<suffix>T1w)(?P<extension>\\.json)\\Z', 'mandatory': False}
assert re.match(json_rule['regex'], 'sub-01/anat/sub-01_T1w.json')
assert re.match(json_rule['regex'], 'sub-01/sub-01_T1w.json')
assert re.match(json_rule['regex'], 'T1w.json')
assert re.match(json_rule['regex'], 'sub-01/ses-01/anat/sub-01_ses-01_T1w.json')
assert re.match(json_rule['regex'], 'sub-01/ses-01/sub-01_ses-01_T1w.json')
assert not re.match(json_rule['regex'], 'sub-01/anat/sub-02_T1w.json')
assert not re.match(json_rule['regex'], 'sub-01_T1w.json')
assert not re.match(json_rule['regex'], 'ses-01_T1w.json')
assert not re.match(json_rule['regex'], 'sub-01/ses-01/anat/sub-01_T1w.json')
assert not re.match(json_rule['regex'], 'sub-01/anat/sub-01_ses-01_T1w.json')
assert not re.match(json_rule['regex'], 'sub-01/ses-01/ses-01_T1w.json')
assert not re.match(json_rule['regex'], 'sub-01/ses-01/anat/sub-01_ses-02_T1w.json')
```

## Next Steps


---

*Source: test_rules.py:8 | Complexity: Intermediate | Last updated: 2026-05-18*