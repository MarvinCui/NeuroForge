# snakemake Source/Test Snippets

Curated implementation snippets recovered from the original generated output. Source paths are upstream-relative or package-relative, never local machine paths.

## 1. test_plugin

- Kind: `test-workflow`
- Source: `snakemake/tests/test_logging.py:289`
- Note: Workflow: Test using a logger plugin. Adds the logging/plugins/ directory to PYTHONPATH so the plugin registry can detect the "snakemake_logger_plugin_test" package. The plugin outputs each record in JSON format on a single line, including the "event" attribute so we can check event counts as in the other tests. The first line is a special record/event that reports information about how Snakemake has configured the handler (such as whether the default formatter or filter were attached). Parameters ---------- stream If True output to stream, otherwise to file. has_formatter Value plugin handler should return for the "has_formatter" property. has_filter Value plugin handler should return for the "has_filter" property. needs_rulegraph Value plugin handler should return for the "needs_rulegraph" property.

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

## 2. test_logger_in_workflow

- Kind: `test-workflow`
- Source: `snakemake/tests/test_logging.py:159`
- Note: Workflow: Test adding a handler to the ``logger`` global in the Snakefile. relevant issue: https://github.com/snakemake/snakemake/issues/3558

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

## 3. test_log_events

- Kind: `test-workflow`
- Source: `snakemake/tests/test_logging.py:218`
- Note: Workflow: Test LogEvent counts of records captured during workflow run.

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

## 4. test_logfile

- Kind: `test-workflow`
- Source: `snakemake/tests/test_logging.py:79`
- Note: Workflow: test logfile

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

## 5. test_single_line_manifest_formatting_not_touched_even_if_wrong

- Kind: `test-workflow`
- Source: `snakemake/tests/test_script.py:219`
- Note: Workflow: The dependency delimiter is wrong, but we let rust-script deal with it

```python
'The dependency delimiter is wrong, but we let rust-script deal with it'
source = dedent('\n// cargo-deps: time="0.1.25"; serde="*"\n// You can also leave off the version number, in which case, it\'s assumed\n// to be "*".  Also, the `cargo-deps` comment *must* be a single-line\n// comment, and it *must* be the first thing in the file, after the\n// shebang.\n// This second dependency line should be ignored\n// cargo-deps: time="0.1.25", libc="0.2.5"\nfn main() {\n    println!("{}", time::now().rfc822z());\n}\n')
manifest, remaining_src = RustScript.extract_manifest(source)
expected_manifest = '\n// cargo-deps: time="0.1.25"; serde="*"\n'
assert manifest == expected_manifest
expected_remaining_src = dedent('// You can also leave off the version number, in which case, it\'s assumed\n// to be "*".  Also, the `cargo-deps` comment *must* be a single-line\n// comment, and it *must* be the first thing in the file, after the\n// shebang.\n// This second dependency line should be ignored\n// cargo-deps: time="0.1.25", libc="0.2.5"\nfn main() {\n    println!("{}", time::now().rfc822z());\n}\n')
assert remaining_src == expected_remaining_src
```

## 6. test_issue4063

- Kind: `test-workflow`
- Source: `snakemake/tests/test_logging.py:106`
- Note: Workflow: test issue4063

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

## 7. test_single_line_manifest_not_at_start_with_shebang

- Kind: `test-workflow`
- Source: `snakemake/tests/test_script.py:43`
- Note: Workflow: test single line manifest not at start with shebang

```python
source = dedent('#!/usr/bin/env rust-script\n// this is where cargo-deps should be\n// cargo-deps: time="0.1.25", serde="*"\n// You can also leave off the version number, in which case, it\'s assumed\n// to be "*".  Also, the `cargo-deps` comment *must* be a single-line\n// comment, and it *must* be the first thing in the file, after the\n// shebang.\n// This second dependency line should be ignored\n// cargo-deps: time="0.1.25", libc="0.2.5"\nfn main() {\n    println!("{}", time::now().rfc822z());\n}\n')
manifest, remaining_src = RustScript.extract_manifest(source)
expected_manifest = ''
assert manifest == expected_manifest
expected_remaining_src = dedent('// this is where cargo-deps should be\n// cargo-deps: time="0.1.25", serde="*"\n// You can also leave off the version number, in which case, it\'s assumed\n// to be "*".  Also, the `cargo-deps` comment *must* be a single-line\n// comment, and it *must* be the first thing in the file, after the\n// shebang.\n// This second dependency line should be ignored\n// cargo-deps: time="0.1.25", libc="0.2.5"\nfn main() {\n    println!("{}", time::now().rfc822z());\n}\n')
assert remaining_src == expected_remaining_src
```

## 8. test_single_line_manifest_not_at_start_without_shebang

- Kind: `test-workflow`
- Source: `snakemake/tests/test_script.py:79`
- Note: Workflow: test single line manifest not at start without shebang

```python
source = dedent('// this is where cargo-deps should be\n// cargo-deps: time="0.1.25", serde="*"\n// You can also leave off the version number, in which case, it\'s assumed\n// to be "*".  Also, the `cargo-deps` comment *must* be a single-line\n// comment, and it *must* be the first thing in the file, after the\n// shebang.\n// This second dependency line should be ignored\n// cargo-deps: time="0.1.25", libc="0.2.5"\nfn main() {\n    println!("{}", time::now().rfc822z());\n}\n')
manifest, remaining_src = RustScript.extract_manifest(source)
expected_manifest = ''
assert manifest == expected_manifest
expected_remaining_src = dedent('// this is where cargo-deps should be\n// cargo-deps: time="0.1.25", serde="*"\n// You can also leave off the version number, in which case, it\'s assumed\n// to be "*".  Also, the `cargo-deps` comment *must* be a single-line\n// comment, and it *must* be the first thing in the file, after the\n// shebang.\n// This second dependency line should be ignored\n// cargo-deps: time="0.1.25", libc="0.2.5"\nfn main() {\n    println!("{}", time::now().rfc822z());\n}\n')
assert remaining_src == expected_remaining_src
```

## 9. test_single_line_manifest_with_shebang_and_second_manifest

- Kind: `test-workflow`
- Source: `snakemake/tests/test_script.py:8`
- Note: Workflow: test single line manifest with shebang and second manifest

```python
source = dedent('#!/usr/bin/env rust-script\n// cargo-deps: time="0.1.25", serde="*"\n// You can also leave off the version number, in which case, it\'s assumed\n// to be "*".  Also, the `cargo-deps` comment *must* be a single-line\n// comment, and it *must* be the first thing in the file, after the\n// shebang.\n// This second dependency line should be ignored\n// cargo-deps: time="0.1.25", libc="0.2.5"\nfn main() {\n    println!("{}", time::now().rfc822z());\n}\n')
manifest, remaining_src = RustScript.extract_manifest(source)
expected_manifest = '// cargo-deps: time="0.1.25", serde="*"\n'
assert manifest == expected_manifest
expected_remaining_src = dedent('// You can also leave off the version number, in which case, it\'s assumed\n// to be "*".  Also, the `cargo-deps` comment *must* be a single-line\n// comment, and it *must* be the first thing in the file, after the\n// shebang.\n// This second dependency line should be ignored\n// cargo-deps: time="0.1.25", libc="0.2.5"\nfn main() {\n    println!("{}", time::now().rfc822z());\n}\n')
assert remaining_src == expected_remaining_src
```

## 10. test_single_line_manifest_spacing_has_no_impact

- Kind: `test-workflow`
- Source: `snakemake/tests/test_script.py:184`
- Note: Workflow: test single line manifest spacing has no impact

```python
source = dedent('\n// cargo-deps : time="0.1.25", serde="*"\n// You can also leave off the version number, in which case, it\'s assumed\n// to be "*".  Also, the `cargo-deps` comment *must* be a single-line\n// comment, and it *must* be the first thing in the file, after the\n// shebang.\n// This second dependency line should be ignored\n// cargo-deps: time="0.1.25", libc="0.2.5"\nfn main() {\n    println!("{}", time::now().rfc822z());\n}\n')
manifest, remaining_src = RustScript.extract_manifest(source)
expected_manifest = '\n// cargo-deps : time="0.1.25", serde="*"\n'
assert manifest == expected_manifest
expected_remaining_src = dedent('// You can also leave off the version number, in which case, it\'s assumed\n// to be "*".  Also, the `cargo-deps` comment *must* be a single-line\n// comment, and it *must* be the first thing in the file, after the\n// shebang.\n// This second dependency line should be ignored\n// cargo-deps: time="0.1.25", libc="0.2.5"\nfn main() {\n    println!("{}", time::now().rfc822z());\n}\n')
assert remaining_src == expected_remaining_src
```

## 11. test_single_line_manifest_is_case_insensitive

- Kind: `test-workflow`
- Source: `snakemake/tests/test_script.py:149`
- Note: Workflow: test single line manifest is case insensitive

```python
source = dedent('\n// Cargo-deps: time="0.1.25", serde="*"\n// You can also leave off the version number, in which case, it\'s assumed\n// to be "*".  Also, the `cargo-deps` comment *must* be a single-line\n// comment, and it *must* be the first thing in the file, after the\n// shebang.\n// This second dependency line should be ignored\n// cargo-deps: time="0.1.25", libc="0.2.5"\nfn main() {\n    println!("{}", time::now().rfc822z());\n}\n')
manifest, remaining_src = RustScript.extract_manifest(source)
expected_manifest = '\n// Cargo-deps: time="0.1.25", serde="*"\n'
assert manifest == expected_manifest
expected_remaining_src = dedent('// You can also leave off the version number, in which case, it\'s assumed\n// to be "*".  Also, the `cargo-deps` comment *must* be a single-line\n// comment, and it *must* be the first thing in the file, after the\n// shebang.\n// This second dependency line should be ignored\n// cargo-deps: time="0.1.25", libc="0.2.5"\nfn main() {\n    println!("{}", time::now().rfc822z());\n}\n')
assert remaining_src == expected_remaining_src
```

## 12. test_single_line_manifest_with_empty_line_without_shebang

- Kind: `test-workflow`
- Source: `snakemake/tests/test_script.py:114`
- Note: Workflow: test single line manifest with empty line without shebang

```python
source = dedent('\n// cargo-deps: time="0.1.25", serde="*"\n// You can also leave off the version number, in which case, it\'s assumed\n// to be "*".  Also, the `cargo-deps` comment *must* be a single-line\n// comment, and it *must* be the first thing in the file, after the\n// shebang.\n// This second dependency line should be ignored\n// cargo-deps: time="0.1.25", libc="0.2.5"\nfn main() {\n    println!("{}", time::now().rfc822z());\n}\n')
manifest, remaining_src = RustScript.extract_manifest(source)
expected_manifest = '\n// cargo-deps: time="0.1.25", serde="*"\n'
assert manifest == expected_manifest
expected_remaining_src = dedent('// You can also leave off the version number, in which case, it\'s assumed\n// to be "*".  Also, the `cargo-deps` comment *must* be a single-line\n// comment, and it *must* be the first thing in the file, after the\n// shebang.\n// This second dependency line should be ignored\n// cargo-deps: time="0.1.25", libc="0.2.5"\nfn main() {\n    println!("{}", time::now().rfc822z());\n}\n')
assert remaining_src == expected_remaining_src
```
