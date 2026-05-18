---
name: snakemake
description: Local codebase analysis for snakemake
doc_version: 
---

# snakemake Codebase

## Description

Local codebase analysis and documentation generated from code analysis.

**Path:** `snakemake`
**Files Analyzed:** 0
**Languages:** 
**Analysis Depth:** surface

## When to Use This Skill

Use this skill when you need to:
- Understand the codebase architecture and design patterns
- Find implementation examples and usage patterns
- Review API documentation extracted from code
- Check configuration patterns and best practices
- Explore test examples and real-world usage
- Navigate the codebase structure efficiently

## ⚡ Quick Reference

### Codebase Statistics

**Languages:**

**Analysis Performed:**
- ✅ API Reference (C2.5)
- ✅ Dependency Graph (C2.6)
- ✅ Design Patterns (C3.1)
- ✅ Test Examples (C3.2)
- ✅ Configuration Patterns (C3.4)
- ✅ Architectural Analysis (C3.7)
- ✅ Project Documentation (C3.9)

### 🎨 Design Patterns Detected

*From C3.1 codebase analysis (confidence > 0.7)*

- **Factory**: 4 instances
- **Adapter**: 3 instances

*Total: 7 high-confidence patterns*

*See `references/patterns/` for complete pattern analysis*

## 📝 Code Examples

*High-quality examples extracted from test files (C3.2)*

**Workflow: test logfile** (complexity: 1.00)

```python
import glob
tmpdir = run(dpath('logging/test_logfile'), cleanup=False, check_results=False)
finished_stmt = '\nFinished jobid: 0 (Rule: all)\n6 of 6 steps (100%) done'
log_dir = os.path.join(tmpdir, '.snakemake', 'log')
assert os.path.exists(log_dir), f'Log directory {log_dir} not found'
log_files = glob.glob(os.path.join(log_dir, '*.snakemake.log'))
assert log_files, 'No log files found'
log_files.sort(key=os.path.getmtime, reverse=True)
latest_log = log_files[0]
with open(latest_log, 'r') as f:
    log_content = f.read()
assert finished_stmt.strip() in log_content.strip(), f'Expected statement not found in log file. Log content: {log_content}'
shutil.rmtree(tmpdir, ignore_errors=ON_WINDOWS)
```

**Workflow: test issue4063** (complexity: 1.00)

```python
from snakemake.logging import ColorizingTextHandler
from snakemake.logging import DefaultFormatter
from snakemake.logging import DefaultFilter
handler = ColorizingTextHandler(stream=sys.stdout)
formatter = DefaultFormatter(quiet=set(), show_failed_logs=False)
handler.setFormatter(formatter)
log_filter = DefaultFilter(quiet=set(), debug_dag=False, dryrun=False, printshellcmds=True)
handler.addFilter(log_filter)

def handle_logging_error(record):
    raise sys.exc_info()[1]
handler.handleError = handle_logging_error
test_logger = logging.getLogger('foo')
test_logger.setLevel(logging.INFO)
test_logger.addHandler(handler)
test_logger.info(None, extra={'event': LogEvent.SHELLCMD, 'cmd': "echo 'bar'"})
test_logger.removeHandler(handler)
```

**Workflow: Test adding a handler to the ``logger`` global in the Snakefile.

relevant issue: https://github.com/snakemake/snakemake/issues/3558** (complexity: 1.00)

```python
'Test adding a handler to the ``logger`` global in the Snakefile.\n\n    relevant issue: https://github.com/snakemake/snakemake/issues/3558\n    '
import glob
tmpdir = run(dpath('logging/test_workflow_logger'), cleanup=False, check_results=False)
stmts = ['TESTINFO', 'TESTWARN', 'TESTERROR']
log_dir = os.path.join(tmpdir, '.snakemake', 'log')
assert os.path.exists(log_dir), f'Log directory {log_dir} not found'
log_files = glob.glob(os.path.join(log_dir, '*.snakemake.log'))
assert log_files, 'No log files found'
log_files.sort(key=os.path.getmtime, reverse=True)
latest_log = log_files[0]
with open(latest_log, 'r') as f:
    log_content = f.read()
custom_log = os.path.join(tmpdir, 'mylog.txt')
with open(custom_log, 'r') as f:
    custom_log_content = f.read()
for stmt in stmts:
    assert stmt.strip() in log_content.strip(), f'Expected statement {stmt} not found in log file. Log content: {log_content}'
    assert stmt.strip() in custom_log_content.strip(), f'Expected statement {stmt} not found in log file. Custom Log content: {custom_log_content}'
shutil.rmtree(tmpdir, ignore_errors=ON_WINDOWS)
```

**Workflow: Test using a logger plugin.

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
    Value plugin handler should return for the "needs_rulegraph" property.** (complexity: 1.00)

```python
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

**Workflow: Test LogEvent counts of records captured during workflow run.** (complexity: 0.80)

```python
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

*See `references/test_examples/` for all extracted examples*

## ⚙️ Configuration Patterns

*From C3.4 configuration analysis*

**Configuration Files Analyzed:** 171
**Total Settings:** 770
**Patterns Detected:** 0

**Configuration Types:**
- unknown: 171 files

*See `references/config_patterns/` for detailed configuration analysis*

## 📖 Project Documentation

*Extracted from markdown files in the project (C3.9)*

**Total Documentation Files:** 78
**Categories:** 8

### Overview

- **README.md** (`README.md`)

### Guides

- **additional_features.rst** (`docs/tutorial/additional_features.rst`)
- **advanced.rst** (`docs/tutorial/advanced.rst`)
- **basics.rst** (`docs/tutorial/basics.rst`)
- **tutorial.rst** (`docs/tutorial/interaction_visualization_reporting/tutorial.rst`)
- **cars.rst** (`docs/tutorial/interaction_visualization_reporting/workdir/workflow/report/cars.rst`)
- *...and 4 more*

### Api

- **module_template.rst** (`apidocs/_templates/module_template.rst`)
- **modules.rst** (`apidocs/api_reference/internal/modules.rst`)
- **snakemake.assets.rst** (`apidocs/api_reference/internal/snakemake.assets.rst`)
- **snakemake.caching.rst** (`apidocs/api_reference/internal/snakemake.caching.rst`)
- **snakemake.common.rst** (`apidocs/api_reference/internal/snakemake.common.rst`)
- *...and 23 more*

### Changelog

- **CHANGELOG.md** (`CHANGELOG.md`)

### Community

- **CODE_OF_CONDUCT.md** (`CODE_OF_CONDUCT.md`)

### License

- **LICENSE.md** (`LICENSE.md`)

*See `references/documentation/` for all project documentation*

## 📚 Available References

This skill includes detailed reference documentation:

- **Dependencies**: `references/dependencies/` - Dependency graph and analysis
- **Patterns**: `references/patterns/` - Detected design patterns
- **Examples**: `references/test_examples/` - Usage examples from tests
- **Configuration**: `references/config_patterns/` - Configuration patterns
- **Documentation**: `references/documentation/` - Project documentation

---

**Generated by Skill Seeker** | Codebase Analyzer with C3.x Analysis
