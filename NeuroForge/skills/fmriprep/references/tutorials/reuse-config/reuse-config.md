# How To: Reuse Config

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test reuse config

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `argparse`
- `contextlib`
- `pytest`
- `packaging.version`
- `tests.test_config`
- `parser`
- `niworkflows.utils.testing`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: Assign bids_dir = value

```python
bids_dir = tmp_path / 'ds000005'
```

**Verification:**
```python
assert default_config['execution.output_spaces'] == 'MNI152NLin2009cAsym:res-native'
```

### Step 2: Call generate_bids_skeleton()

```python
generate_bids_skeleton(bids_dir, {'01': {'anat': {'suffix': 'T1w'}}})
```

**Verification:**
```python
assert reused_config['execution.output_spaces'] == 'MNI152NLin2009cAsym:res-2 MNI152NLin2009cAsym:res-native fsaverage:den-10k fsaverage:den-30k'
```

### Step 3: Assign cli_args = value

```python
cli_args = [str(bids_dir), str(tmp_path / 'out'), 'participant', '--skip-bids-validation']
```

**Verification:**
```python
assert reused_config['execution.log_dir'] not in config_file.read_text()
```

### Step 4: Call parse_args()

```python
parse_args(cli_args)
```

**Verification:**
```python
assert overridden_config['execution.output_spaces'] == 'MNI152NLin6Asym:res-native'
```

### Step 5: Assign default_config = config.get(...)

```python
default_config = config.get(flat=True)
```

**Verification:**
```python
assert 'bbr' in overridden_config['workflow.force']
```

### Step 6: Call _reset_config()

```python
_reset_config()
```

**Verification:**
```python
assert reused_config[v] != overridden_config[v]
```

### Step 7: Assign config_file = data.load(...)

```python
config_file = data.load('tests/config.toml')
```

### Step 8: Assign config_args = value

```python
config_args = ['--config-file', str(config_file)]
```

### Step 9: Call parse_args()

```python
parse_args(cli_args + config_args)
```

### Step 10: Assign reused_config = config.get(...)

```python
reused_config = config.get(flat=True)
```

**Verification:**
```python
assert reused_config['execution.output_spaces'] == 'MNI152NLin2009cAsym:res-2 MNI152NLin2009cAsym:res-native fsaverage:den-10k fsaverage:den-30k'
```

### Step 11: Call _reset_config()

```python
_reset_config()
```

### Step 12: Assign overridden_args = value

```python
overridden_args = cli_args + config_args + ['--output-spaces', 'MNI152NLin6Asym', '--force', 'bbr']
```

### Step 13: Assign unknown = str(...)

```python
overridden_args[1] = str(tmp_path / 'out2')
```

### Step 14: Call parse_args()

```python
parse_args(overridden_args)
```

### Step 15: Assign overridden_config = config.get(...)

```python
overridden_config = config.get(flat=True)
```

**Verification:**
```python
assert overridden_config['execution.output_spaces'] == 'MNI152NLin6Asym:res-native'
```

### Step 16: Call _reset_config()

```python
_reset_config()
```

**Verification:**
```python
assert reused_config[v] != overridden_config[v]
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
from niworkflows.utils.testing import generate_bids_skeleton
bids_dir = tmp_path / 'ds000005'
generate_bids_skeleton(bids_dir, {'01': {'anat': {'suffix': 'T1w'}}})
cli_args = [str(bids_dir), str(tmp_path / 'out'), 'participant', '--skip-bids-validation']
parse_args(cli_args)
default_config = config.get(flat=True)
assert default_config['execution.output_spaces'] == 'MNI152NLin2009cAsym:res-native'
_reset_config()
config_file = data.load('tests/config.toml')
config_args = ['--config-file', str(config_file)]
parse_args(cli_args + config_args)
reused_config = config.get(flat=True)
assert reused_config['execution.output_spaces'] == 'MNI152NLin2009cAsym:res-2 MNI152NLin2009cAsym:res-native fsaverage:den-10k fsaverage:den-30k'
assert reused_config['execution.log_dir'] not in config_file.read_text()
_reset_config()
overridden_args = cli_args + config_args + ['--output-spaces', 'MNI152NLin6Asym', '--force', 'bbr']
overridden_args[1] = str(tmp_path / 'out2')
parse_args(overridden_args)
overridden_config = config.get(flat=True)
assert overridden_config['execution.output_spaces'] == 'MNI152NLin6Asym:res-native'
assert 'bbr' in overridden_config['workflow.force']
for v in ('execution.run_uuid', 'execution.fmriprep_dir'):
    assert reused_config[v] != overridden_config[v]
_reset_config()
```

## Next Steps


---

*Source: test_parser.py:292 | Complexity: Advanced | Last updated: 2026-05-18*