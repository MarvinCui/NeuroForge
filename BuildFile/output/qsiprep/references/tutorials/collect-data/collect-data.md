# How To: Collect Data

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test qsiprep.utils.bids.collect_data.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pytest`
- `niworkflows.utils.testing`
- `re`
- `bids.layout`
- `qsiprep`
- `qsiprep.cli.parser`
- `pprint`
- `qsiprep.utils.bids`

**Setup Required:**
```python
# Fixtures: tmpdir, name, skeleton, sessions, n_anats
```

## Step-by-Step Guide

### Step 1: 'Test qsiprep.utils.bids.collect_data.'

```python
'Test qsiprep.utils.bids.collect_data.'
```

**Verification:**
```python
assert len(subj_data['t1w']) == n_anats[0], pprint.pformat(subj_data)
```

### Step 2: Assign bids_dir = value

```python
bids_dir = tmpdir / name
```

**Verification:**
```python
assert len(subj_data['t1w']) == n_anats[1], pprint.pformat(subj_data)
```

### Step 3: Call generate_bids_skeleton()

```python
generate_bids_skeleton(str(bids_dir), skeleton)
```

**Verification:**
```python
assert len(subj_data['t1w']) == n_anats[2], pprint.pformat(subj_data)
```

### Step 4: Assign participant_label = '01'

```python
participant_label = '01'
```

**Verification:**
```python
assert len(subj_data['t2w']) == 0, pprint.pformat(subj_data)
```

### Step 5: Assign subj_data = value

```python
subj_data = collect_data(bids_dir=str(bids_dir), participant_label=participant_label, session_id=sessions[0], filters=None, bids_validate=False, ignore=[])[0]
```

**Verification:**
```python
assert len(subj_data['t1w']) == n_anats[0], pprint.pformat(subj_data)
```

### Step 6: Assign subj_data = value

```python
subj_data = collect_data(bids_dir=str(bids_dir), participant_label=participant_label, session_id=sessions[1], filters=None, bids_validate=False, ignore=[])[0]
```

**Verification:**
```python
assert len(subj_data['t1w']) == n_anats[1], pprint.pformat(subj_data)
```

### Step 7: Assign subj_data = value

```python
subj_data = collect_data(bids_dir=str(bids_dir), participant_label=participant_label, session_id=sessions, filters=None, bids_validate=False, ignore=['t2w'])[0]
```

**Verification:**
```python
assert len(subj_data['t1w']) == n_anats[2], pprint.pformat(subj_data)
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir, name, skeleton, sessions, n_anats

# Workflow
'Test qsiprep.utils.bids.collect_data.'
import pprint
from qsiprep.utils.bids import collect_data
bids_dir = tmpdir / name
generate_bids_skeleton(str(bids_dir), skeleton)
participant_label = '01'
subj_data = collect_data(bids_dir=str(bids_dir), participant_label=participant_label, session_id=sessions[0], filters=None, bids_validate=False, ignore=[])[0]
assert len(subj_data['t1w']) == n_anats[0], pprint.pformat(subj_data)
subj_data = collect_data(bids_dir=str(bids_dir), participant_label=participant_label, session_id=sessions[1], filters=None, bids_validate=False, ignore=[])[0]
assert len(subj_data['t1w']) == n_anats[1], pprint.pformat(subj_data)
subj_data = collect_data(bids_dir=str(bids_dir), participant_label=participant_label, session_id=sessions, filters=None, bids_validate=False, ignore=['t2w'])[0]
assert len(subj_data['t1w']) == n_anats[2], pprint.pformat(subj_data)
assert len(subj_data['t2w']) == 0, pprint.pformat(subj_data)
```

## Next Steps


---

*Source: test_cli_run.py:201 | Complexity: Intermediate | Last updated: 2026-05-18*