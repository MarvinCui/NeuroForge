# How To: Plugin

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test using a logger plugin.

Adds the logging/plugins/ directory to PYTHONPATH so the plugin registry can detect the
"snakemake_logger_plugin_test" package. The plugin outputs each record in JSON format on a
single line, including the "event" attribute so we can check event counts as in the other tests.
The first line is a special record/event that reports information about how Snakemake has
configured the handler (such as whether the default formatter or filter were attached).

Parameters
----------
stream
    If True output to stream, otherwise to file.
has_formatter
    Value plugin handler should return for the "has_formatter" property.
has_filter
    Value plugin handler should return for the "has_filter" property.
needs_rulegraph
    Value plugin handler should return for the "needs_rulegraph" property.

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
# Fixtures: stream, has_formatter, has_filter, needs_rulegraph, tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test using a logger plugin.\n\n    Adds the logging/plugins/ directory to PYTHONPATH so the plugin registry can detect the\n    "snakemake_logger_plugin_test" package. The plugin outputs each record in JSON format on a\n    single line, including the "event" attribute so we can check event counts as in the other tests.\n    The first line is a special record/event that reports information about how Snakemake has\n    configured the handler (such as whether the default formatter or filter were attached).\n\n    Parameters\n    ----------\n    stream\n        If True output to stream, otherwise to file.\n    has_formatter\n        Value plugin handler should return for the "has_formatter" property.\n    has_filter\n        Value plugin handler should return for the "has_filter" property.\n    needs_rulegraph\n        Value plugin handler should return for the "needs_rulegraph" property.\n    '

```python
'Test using a logger plugin.\n\n    Adds the logging/plugins/ directory to PYTHONPATH so the plugin registry can detect the\n    "snakemake_logger_plugin_test" package. The plugin outputs each record in JSON format on a\n    single line, including the "event" attribute so we can check event counts as in the other tests.\n    The first line is a special record/event that reports information about how Snakemake has\n    configured the handler (such as whether the default formatter or filter were attached).\n\n    Parameters\n    ----------\n    stream\n        If True output to stream, otherwise to file.\n    has_formatter\n        Value plugin handler should return for the "has_formatter" property.\n    has_filter\n        Value plugin handler should return for the "has_filter" property.\n    needs_rulegraph\n        Value plugin handler should return for the "needs_rulegraph" property.\n    '
```

**Verification:**
```python
assert records[0]['event'] == 'logger_info'
```

### Step 2: Assign plugin_dir = dpath(...)

```python
plugin_dir = dpath('logging/plugins')
```

**Verification:**
```python
assert records[0]['formatter_set'] == (not has_formatter)
```

### Step 3: Assign test_dir = dpath(...)

```python
test_dir = dpath('logging/test_logfile')
```

**Verification:**
```python
assert records[0]['filter_added'] == (not has_filter)
```

### Step 4: Assign outfile = value

```python
outfile = tmp_path / 'out.log'
```

### Step 5: Assign env = dict(...)

```python
env = dict(os.environ)
```

### Step 6: Assign current_path = env.get(...)

```python
current_path = env.get('PYTHONPATH')
```

### Step 7: Assign unknown = value

```python
env['PYTHONPATH'] = str(plugin_dir) if current_path is None else str(plugin_dir) + os.pathsep + current_path
```

### Step 8: Assign cmd = value

```python
cmd = [sys.executable, '-m', 'snakemake', '-s', str(test_dir / 'Snakefile'), '-j1', '--verbose', '--printshellcmds', '--logger', 'test']
```

### Step 9: Assign result = sp.run(...)

```python
result = sp.run(cmd, cwd=tmp_path, env=env, check=True, capture_output=stream, text=True)
```

**Verification:**
```python
assert records[0]['event'] == 'logger_info'
```

### Step 10: Assign event_counts = Counter(...)

```python
event_counts = Counter((LogEvent[record['event'].upper()] for record in records[1:] if record['event']))
```

### Step 11: Call check_event_counts()

```python
check_event_counts(event_counts, {LogEvent.RUN_INFO: 1, LogEvent.JOB_INFO: 6, LogEvent.SHELLCMD: 6, LogEvent.RESOURCES_INFO: 2, LogEvent.PROGRESS: 6, LogEvent.JOB_STARTED: None, LogEvent.JOB_FINISHED: 6, LogEvent.WORKFLOW_STARTED: 1 if has_filter else 0, LogEvent.DEBUG_DAG: None if has_filter else 0, LogEvent.RULEGRAPH: 1 if needs_rulegraph else 0})
```

### Step 12: Call cmd.extend()

```python
cmd.extend(['--logger-test-outfile', outfile.name])
```

### Step 13: Call cmd.append()

```python
cmd.append('--logger-test-has-formatter')
```

### Step 14: Call cmd.append()

```python
cmd.append('--logger-test-has-filter')
```

### Step 15: Call cmd.append()

```python
cmd.append('--logger-test-needs-rulegraph')
```

### Step 16: Assign records = list(...)

```python
records = list(map(json.loads, result.stderr.splitlines()))
```

### Step 17: Assign records = list(...)

```python
records = list(map(json.loads, fh))
```


## Complete Example

```python
# Setup
# Fixtures: stream, has_formatter, has_filter, needs_rulegraph, tmp_path

# Workflow
'Test using a logger plugin.\n\n    Adds the logging/plugins/ directory to PYTHONPATH so the plugin registry can detect the\n    "snakemake_logger_plugin_test" package. The plugin outputs each record in JSON format on a\n    single line, including the "event" attribute so we can check event counts as in the other tests.\n    The first line is a special record/event that reports information about how Snakemake has\n    configured the handler (such as whether the default formatter or filter were attached).\n\n    Parameters\n    ----------\n    stream\n        If True output to stream, otherwise to file.\n    has_formatter\n        Value plugin handler should return for the "has_formatter" property.\n    has_filter\n        Value plugin handler should return for the "has_filter" property.\n    needs_rulegraph\n        Value plugin handler should return for the "needs_rulegraph" property.\n    '
plugin_dir = dpath('logging/plugins')
test_dir = dpath('logging/test_logfile')
outfile = tmp_path / 'out.log'
env = dict(os.environ)
current_path = env.get('PYTHONPATH')
env['PYTHONPATH'] = str(plugin_dir) if current_path is None else str(plugin_dir) + os.pathsep + current_path
cmd = [sys.executable, '-m', 'snakemake', '-s', str(test_dir / 'Snakefile'), '-j1', '--verbose', '--printshellcmds', '--logger', 'test']
if not stream:
    cmd.extend(['--logger-test-outfile', outfile.name])
if has_formatter:
    cmd.append('--logger-test-has-formatter')
if has_filter:
    cmd.append('--logger-test-has-filter')
if needs_rulegraph:
    cmd.append('--logger-test-needs-rulegraph')
result = sp.run(cmd, cwd=tmp_path, env=env, check=True, capture_output=stream, text=True)
if stream:
    records = list(map(json.loads, result.stderr.splitlines()))
else:
    with open(outfile) as fh:
        records = list(map(json.loads, fh))
assert records[0]['event'] == 'logger_info'
assert records[0]['formatter_set'] == (not has_formatter)
assert records[0]['filter_added'] == (not has_filter)
event_counts = Counter((LogEvent[record['event'].upper()] for record in records[1:] if record['event']))
check_event_counts(event_counts, {LogEvent.RUN_INFO: 1, LogEvent.JOB_INFO: 6, LogEvent.SHELLCMD: 6, LogEvent.RESOURCES_INFO: 2, LogEvent.PROGRESS: 6, LogEvent.JOB_STARTED: None, LogEvent.JOB_FINISHED: 6, LogEvent.WORKFLOW_STARTED: 1 if has_filter else 0, LogEvent.DEBUG_DAG: None if has_filter else 0, LogEvent.RULEGRAPH: 1 if needs_rulegraph else 0})
```

## Next Steps


---

*Source: test_logging.py:289 | Complexity: Advanced | Last updated: 2026-05-18*