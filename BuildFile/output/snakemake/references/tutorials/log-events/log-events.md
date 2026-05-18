# How To: Log Events

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test LogEvent counts of records captured during workflow run.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `shutil`
- `sys`
- `subprocess`
- `logging`
- `logging.handlers`
- `collections`
- `pathlib`
- `queue`
- `json`
- `pytest`
- `snakemake_interface_logger_plugins.common`
- `common`
- `conftest`
- `glob`
- `snakemake.logging`
- `snakemake.logging`
- `snakemake.logging`
- `glob`
- `snakemake.logging`
- `snakemake.settings.types`

**Setup Required:**
```python
# Fixtures: caplog, capfd
```

## Step-by-Step Guide

### Step 1: 'Test LogEvent counts of records captured during workflow run.'

```python
'Test LogEvent counts of records captured during workflow run.'
```

**Verification:**
```python
assert expected_msg in stderr_output, f"Expected '{expected_msg}' not found in stderr output"
```

### Step 2: Assign event_counts = count_events(...)

```python
event_counts = count_events(caplog)
```

### Step 3: Call check_event_counts()

```python
check_event_counts(event_counts, {LogEvent.WORKFLOW_STARTED: 1, LogEvent.RUN_INFO: 1, LogEvent.JOB_INFO: 6, LogEvent.SHELLCMD: 6, LogEvent.RESOURCES_INFO: 2, LogEvent.PROGRESS: 6, LogEvent.JOB_STARTED: None, LogEvent.JOB_FINISHED: 6})
```

### Step 4: Assign captured = capfd.readouterr(...)

```python
captured = capfd.readouterr()
```

### Step 5: Assign stderr_output = value

```python
stderr_output = captured.err
```

### Step 6: Assign expected_in_stderr = value

```python
expected_in_stderr = ['Building DAG of jobs', 'Job stats:', 'Finished job', 'localrule all:']
```

### Step 7: Call run()

```python
run(dpath('logging/test_logfile'), check_results=False)
```

**Verification:**
```python
assert expected_msg in stderr_output, f"Expected '{expected_msg}' not found in stderr output"
```


## Complete Example

```python
# Setup
# Fixtures: caplog, capfd

# Workflow
'Test LogEvent counts of records captured during workflow run.'
with caplog.at_level(logging.INFO):
    run(dpath('logging/test_logfile'), check_results=False)
event_counts = count_events(caplog)
check_event_counts(event_counts, {LogEvent.WORKFLOW_STARTED: 1, LogEvent.RUN_INFO: 1, LogEvent.JOB_INFO: 6, LogEvent.SHELLCMD: 6, LogEvent.RESOURCES_INFO: 2, LogEvent.PROGRESS: 6, LogEvent.JOB_STARTED: None, LogEvent.JOB_FINISHED: 6})
captured = capfd.readouterr()
stderr_output = captured.err
expected_in_stderr = ['Building DAG of jobs', 'Job stats:', 'Finished job', 'localrule all:']
for expected_msg in expected_in_stderr:
    assert expected_msg in stderr_output, f"Expected '{expected_msg}' not found in stderr output"
```

## Next Steps


---

*Source: test_logging.py:218 | Complexity: Intermediate | Last updated: 2026-05-18*