# How To: Code Block Manifest Spacing Around Language

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test code block manifest spacing around language

## Prerequisites

**Required Modules:**
- `textwrap`
- `snakemake.iocontainers`
- `snakemake.script`


## Step-by-Step Guide

### Step 1: Assign source = dedent(...)

```python
source = dedent('\n//! This is a regular crate doc comment, but it also contains a partial\n//! Cargo manifest.  Note the use of a *fenced* code block, and the\n//! `cargo` "language".\n//!\n//! ```  cargo\n//! [dependencies]\n//! time = "0.1.25"\n//! ```\nfn main() {\n    println!("{}", time::now().rfc822z());\n}\n\n')
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

### Step 3: Assign expected_manifest = dedent(...)

```python
expected_manifest = dedent('\n//! This is a regular crate doc comment, but it also contains a partial\n//! Cargo manifest.  Note the use of a *fenced* code block, and the\n//! `cargo` "language".\n//!\n//! ```  cargo\n//! [dependencies]\n//! time = "0.1.25"\n//! ```\n')
```

**Verification:**
```python
assert manifest == expected_manifest
```

### Step 4: Assign expected_remaining_src = dedent(...)

```python
expected_remaining_src = dedent('fn main() {\n    println!("{}", time::now().rfc822z());\n}\n\n')
```

**Verification:**
```python
assert remaining_src == expected_remaining_src
```


## Complete Example

```python
# Workflow
source = dedent('\n//! This is a regular crate doc comment, but it also contains a partial\n//! Cargo manifest.  Note the use of a *fenced* code block, and the\n//! `cargo` "language".\n//!\n//! ```  cargo\n//! [dependencies]\n//! time = "0.1.25"\n//! ```\nfn main() {\n    println!("{}", time::now().rfc822z());\n}\n\n')
manifest, remaining_src = RustScript.extract_manifest(source)
expected_manifest = dedent('\n//! This is a regular crate doc comment, but it also contains a partial\n//! Cargo manifest.  Note the use of a *fenced* code block, and the\n//! `cargo` "language".\n//!\n//! ```  cargo\n//! [dependencies]\n//! time = "0.1.25"\n//! ```\n')
assert manifest == expected_manifest
expected_remaining_src = dedent('fn main() {\n    println!("{}", time::now().rfc822z());\n}\n\n')
assert remaining_src == expected_remaining_src
```

## Next Steps


---

*Source: test_script.py:359 | Complexity: Intermediate | Last updated: 2026-05-18*