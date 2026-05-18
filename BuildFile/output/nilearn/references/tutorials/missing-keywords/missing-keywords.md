# How To: Missing Keywords

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Check the strategy keywords are raising errors correctly in low        and high level functions.
    

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pandas`
- `pytest`
- `nilearn.interfaces.fmriprep`
- `nilearn.interfaces.fmriprep.load_confounds`
- `nilearn.interfaces.fmriprep.load_confounds_utils`
- `nilearn.interfaces.fmriprep.tests._testing`

**Setup Required:**
```python
# Fixtures: tmp_path, strategy_keywords, expected_parameters, fmriprep_version
```

## Step-by-Step Guide

### Step 1: 'Check the strategy keywords are raising errors correctly in low        and high level functions.\n    '

```python
'Check the strategy keywords are raising errors correctly in low        and high level functions.\n    '
```

**Verification:**
```python
assert confounds_unit_test.empty is True
```

### Step 2: Assign unknown = create_tmp_filepath(...)

```python
img, bad_conf = create_tmp_filepath(tmp_path, copy_confounds=True, copy_json=True, fmriprep_version=fmriprep_version)
```

**Verification:**
```python
assert missing['keywords'] == [strategy_keywords]
```

### Step 3: Assign legal_confounds = pd.read_csv(...)

```python
legal_confounds = pd.read_csv(bad_conf, delimiter='\t', encoding='utf-8')
```

**Verification:**
```python
assert strategy_keywords in exc_info.value.args[0]
```

### Step 4: Assign meta_json = value

```python
meta_json = bad_conf.parent / bad_conf.name.replace('tsv', 'json')
```

### Step 5: Assign meta_json = load_confounds_json(...)

```python
meta_json = load_confounds_json(meta_json, flag_acompcor=True)
```

### Step 6: Assign unknown = _load_noise_component(...)

```python
remove_columns, missing = _load_noise_component(legal_confounds, component=strategy_keywords, missing={'confounds': [], 'keywords': []}, meta_json=meta_json, **expected_parameters)
```

### Step 7: Assign confounds_raw = legal_confounds.drop(...)

```python
confounds_raw = legal_confounds.drop(columns=remove_columns)
```

### Step 8: Call confounds_raw.to_csv()

```python
confounds_raw.to_csv(bad_conf, sep='\t', index=False)
```

### Step 9: Assign missing = value

```python
missing = {'confounds': [], 'keywords': []}
```

### Step 10: Assign unknown = _load_noise_component(...)

```python
confounds_unit_test, missing = _load_noise_component(confounds_raw, component=strategy_keywords, missing=missing, meta_json=meta_json, **expected_parameters)
```

**Verification:**
```python
assert confounds_unit_test.empty is True
```

### Step 11: Call load_confounds()

```python
load_confounds(img, strategy=[strategy_keywords], **expected_parameters)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, strategy_keywords, expected_parameters, fmriprep_version

# Workflow
'Check the strategy keywords are raising errors correctly in low        and high level functions.\n    '
img, bad_conf = create_tmp_filepath(tmp_path, copy_confounds=True, copy_json=True, fmriprep_version=fmriprep_version)
legal_confounds = pd.read_csv(bad_conf, delimiter='\t', encoding='utf-8')
meta_json = bad_conf.parent / bad_conf.name.replace('tsv', 'json')
meta_json = load_confounds_json(meta_json, flag_acompcor=True)
remove_columns, missing = _load_noise_component(legal_confounds, component=strategy_keywords, missing={'confounds': [], 'keywords': []}, meta_json=meta_json, **expected_parameters)
confounds_raw = legal_confounds.drop(columns=remove_columns)
confounds_raw.to_csv(bad_conf, sep='\t', index=False)
missing = {'confounds': [], 'keywords': []}
confounds_unit_test, missing = _load_noise_component(confounds_raw, component=strategy_keywords, missing=missing, meta_json=meta_json, **expected_parameters)
assert confounds_unit_test.empty is True
assert missing['keywords'] == [strategy_keywords]
with pytest.raises(ValueError) as exc_info:
    load_confounds(img, strategy=[strategy_keywords], **expected_parameters)
assert strategy_keywords in exc_info.value.args[0]
```

## Next Steps


---

*Source: test_load_confounds_components.py:32 | Complexity: Advanced | Last updated: 2026-05-18*