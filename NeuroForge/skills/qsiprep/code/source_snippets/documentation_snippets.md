# qsiprep Documentation Snippets

Curated implementation snippets recovered from the original generated output. Source paths are upstream-relative or package-relative, never local machine paths.

## 1. AGENTS.md -- QSIPrep

- Kind: `documentation`
- Source: `references/documentation/overview/AGENTS.md`
- Note: Documentation code block extracted for implementation use.

```python
from <pkg> import config

# Read a setting
work_dir = config.execution.work_dir

# Serialize to disk
config.to_filename(path)

# Load from disk (in a subprocess)
config.load(path)
```

## 2. Contributors #2

- Kind: `documentation`
- Source: `references/documentation/other/contributors.rst`
- Note: Documentation code block extracted for implementation use.

```text
$ python run_local_tests.py -m "dsdti_fmap"
$ python run_local_tests.py -k "test_some_name"
```

## 3. Contributors #1

- Kind: `documentation`
- Source: `references/documentation/other/contributors.rst`
- Note: Documentation code block extracted for implementation use.

```text
$ cd /path/to/qsiprep/qsiprep/tests
$ python run_local_tests.py
```

## 4. Contributors #3

- Kind: `documentation`
- Source: `references/documentation/other/contributors.rst`
- Note: Documentation code block extracted for implementation use.

```text
workflow = Workflow(name=name)
```

## 5. Preprocessing #1

- Kind: `documentation`
- Source: `references/documentation/other/preprocessing.rst`
- Note: Documentation code block extracted for implementation use.

```text
wf = init_anat_preproc_wf(
```

## 6. Preprocessing #2

- Kind: `documentation`
- Source: `references/documentation/other/preprocessing.rst`
- Note: Documentation code block extracted for implementation use.

```text
wf = init_dwi_preproc_wf(
```

## 7. Preprocessing #3

- Kind: `documentation`
- Source: `references/documentation/other/preprocessing.rst`
- Note: Documentation code block extracted for implementation use.

```text
wf = init_fsl_hmc_wf(
```
