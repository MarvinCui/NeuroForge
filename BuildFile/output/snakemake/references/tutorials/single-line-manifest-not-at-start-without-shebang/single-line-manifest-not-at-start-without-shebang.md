# How To: Single Line Manifest Not At Start Without Shebang

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test single line manifest not at start without shebang

## Prerequisites

**Required Modules:**
- `textwrap`
- `snakemake.iocontainers`
- `snakemake.script`


## Step-by-Step Guide

### Step 1: Assign source = dedent(...)

```python
source = dedent('// this is where cargo-deps should be\n// cargo-deps: time="0.1.25", serde="*"\n// You can also leave off the version number, in which case, it\'s assumed\n// to be "*".  Also, the `cargo-deps` comment *must* be a single-line\n// comment, and it *must* be the first thing in the file, after the\n// shebang.\n// This second dependency line should be ignored\n// cargo-deps: time="0.1.25", libc="0.2.5"\nfn main() {\n    println!("{}", time::now().rfc822z());\n}\n')
```

**Verification:**
```python
assert manifest == expected_manifest
```

### Step 2: Assign unknown = RustScript.extract_manifest(...)

```python
manifest, remaining_src = RustScript.extract_manifest(source)
```

**Verification:**
```python
assert remaining_src == expected_remaining_src
```

### Step 3: Assign expected_manifest = ''

```python
expected_manifest = ''
```

**Verification:**
```python
assert manifest == expected_manifest
```

### Step 4: Assign expected_remaining_src = dedent(...)

```python
expected_remaining_src = dedent('// this is where cargo-deps should be\n// cargo-deps: time="0.1.25", serde="*"\n// You can also leave off the version number, in which case, it\'s assumed\n// to be "*".  Also, the `cargo-deps` comment *must* be a single-line\n// comment, and it *must* be the first thing in the file, after the\n// shebang.\n// This second dependency line should be ignored\n// cargo-deps: time="0.1.25", libc="0.2.5"\nfn main() {\n    println!("{}", time::now().rfc822z());\n}\n')
```

**Verification:**
```python
assert remaining_src == expected_remaining_src
```


## Complete Example

```python
# Workflow
source = dedent('// this is where cargo-deps should be\n// cargo-deps: time="0.1.25", serde="*"\n// You can also leave off the version number, in which case, it\'s assumed\n// to be "*".  Also, the `cargo-deps` comment *must* be a single-line\n// comment, and it *must* be the first thing in the file, after the\n// shebang.\n// This second dependency line should be ignored\n// cargo-deps: time="0.1.25", libc="0.2.5"\nfn main() {\n    println!("{}", time::now().rfc822z());\n}\n')
manifest, remaining_src = RustScript.extract_manifest(source)
expected_manifest = ''
assert manifest == expected_manifest
expected_remaining_src = dedent('// this is where cargo-deps should be\n// cargo-deps: time="0.1.25", serde="*"\n// You can also leave off the version number, in which case, it\'s assumed\n// to be "*".  Also, the `cargo-deps` comment *must* be a single-line\n// comment, and it *must* be the first thing in the file, after the\n// shebang.\n// This second dependency line should be ignored\n// cargo-deps: time="0.1.25", libc="0.2.5"\nfn main() {\n    println!("{}", time::now().rfc822z());\n}\n')
assert remaining_src == expected_remaining_src
```

## Next Steps


---

*Source: test_script.py:79 | Complexity: Intermediate | Last updated: 2026-05-18*